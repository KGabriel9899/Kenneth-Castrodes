<template>
    <div class="w-full max-w-xs mx-auto">
        <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" v-on:submit.prevent="login_cred()" method="POST">
            <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
                Username
            </label>
            <input required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" v-model="username" type="text" placeholder="Username">
            </div>
            <div class="mb-6">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
                Password
            </label>
            <input required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" v-model="password" type="password" placeholder="******************">
            </div>
            <div class="flex items-center justify-between">
            <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">
                Log In
            </button>
            </div>
        </form>
    </div>
    <div class="hidden min-w-screen h-screen animated fadeIn faster  fixed left-0 top-0 flex justify-center items-center inset-0 z-50 outline-none focus:outline-none bg-no-repeat bg-center bg-cover" id="modal-id">
   	  <div class="absolute bg-black opacity-80 inset-0 z-0"></div>      
        <div id="popup-modal" tabindex="-1" class="flex top-0 left-0 right-0 z-50 p-4 overflow-x-hidden overflow-y-auto md:inset-0 h-[calc(100%-1rem)] max-h-full">
            <div class="relative w-full max-w-md max-h-full flex-col">
                <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
                    <button type="button" class="absolute top-3 right-2.5 text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 ml-auto inline-flex items-center dark:hover:bg-gray-800 dark:hover:text-white" @click="close_modal">
                        <svg aria-hidden="true" class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
                        <span class="sr-only">Close modal</span>
                    </button>
                    <div class="p-6 text-center">
                        <svg aria-hidden="true" class="mx-auto mb-4 text-gray-400 w-14 h-14 dark:text-gray-200" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                        <h3 class="mb-5 text-lg font-normal text-gray-500 dark:text-gray-400">
                          User does not found!
                        </h3>
                        <button @click="close_modal" type="button" class="text-white bg-red-600 hover:bg-red-800 focus:ring-4 focus:outline-none focus:ring-red-300 dark:focus:ring-red-800 font-medium rounded-lg text-sm inline-flex items-center px-5 py-2.5 text-center mr-2">
                            Okay
                        </button>
                        <button @click="red_signup" type="button" class="text-gray-500 bg-white hover:bg-gray-100 focus:ring-4 focus:outline-none focus:ring-gray-200 rounded-lg border border-gray-200 text-sm font-medium px-5 py-2.5 hover:text-gray-900 focus:z-10 dark:bg-gray-700 dark:text-gray-300 dark:border-gray-500 dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-gray-600">
                          Sign Up
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
let isLoggedIn = '';
export default {
  data() {
    return {
      username: '',
      password: ''
    }
  },
  props: {
    msg: String
  },
  mounted() {
    isLoggedIn = localStorage.getItem('jwt_token')
    if (isLoggedIn) {
      let route = this.$router.resolve({ path: "/" });
      window.open(route.href,"_self");
    }
  },
  methods: {
    login_cred(event) {
      let acc = false;
      let data_name = '';
      let data = {
          identifier: this.username,
          password: this.password
        };
      
        this.password = '';
        console.log("this.password");

      axios.post('http://localhost:1337/api/auth/local', data).then(response => {
        // Handle success.
        console.log(response.data.jwt);
        console.log(response.data.user.id);

        // Store JWT_TOKEN in Local Storage
        localStorage.setItem('jwt_token', response.data.jwt);

        const options = {
          method: 'GET',
          url: 'http://localhost:1337/api/user-log-creds/' + response.data.user.id,
          headers: {
            Authorization: 'Bearer ' + response.data.jwt
          }
        };

        axios.request(options).then(async function (responsen) {
          data_name = responsen.data.data.attributes.firstname + ' ' + responsen.data.data.attributes.lastname;
          console.log(data_name);
         
          // Store name in Local Storage
          localStorage.setItem('name', data_name);

          // Navigate to Home
          window.open("http://localhost:3000/","_self");
        }).catch(function (error) {
          console.error(error);
        });
      }).catch(error => {
        // Handle error.

        // Popup alert modal
        document.getElementById("modal-id").style.display= "flex";
        this.password = '';
      });
    },
    close_modal(event){
      document.getElementById("modal-id").style.display= "none";
      this.password = '';
      localStorage.clear();
    },
    red_signup(event){
      document.getElementById("modal-id").style.display= "none";
      this.password = '';
      this.username = '';
      console.log("Redirect to Signup");
      let route = this.$router.resolve({ path: "/signup" });
      window.open(route.href,"_self");
    }
  }
}
</script>

<style scoped>
</style>