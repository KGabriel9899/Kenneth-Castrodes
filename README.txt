Installation for Nuxt app
    -Node version 16 or newer
    -Open a terminal and use the following command to create a new starter project:
    -For this project, the name of the app is logform-app
        >npx nuxi init logform-app
        >cd logform-app
        >npm install (to install dependencies)
        >npm run dev (to run your nuxt from your browser with the localhost address)
        >npm install --save-dev @nuxtjs/tailwindcss
        >npm install --save axios vue-axios
Installation for Strapi
    -Open terminal of your root file project and use the following command to install the strapi folder/project
    -The name of your strapi folder for this project is logform-backend
        >npx create-strapi-app logform-backend
        >npm run develop
    -then setup your strapi

Create Layout for your Nuxt app
-logform-app/layouts/default.vue

<template>
    <div>
      <header class="shadow-sm bg-white">
        <nav class="container mx-auto p-4 flex justify-end">
          <ul class="flex gap-4">
            <li><NuxtLink to="/">Home</NuxtLink></li>
            <li class="nuxtLogged"><NuxtLink to="/logout">Log out</NuxtLink></li>
            <li class="nuxtDefault"><NuxtLink to="/login">Login</NuxtLink></li>
            <li class="nuxtDefault"><NuxtLink to="/signup">Sign Up</NuxtLink></li>
          </ul>
        </nav>
      </header>
    </div>
  
    <div class="container mx-auto p-4">
      <slot />
    </div>
</template>
  
<script>
  export default {
    data() {
      return {
        tok: '',
      }
    },
    mounted() {
      this.tok = localStorage.getItem('name')
      const defaultLinks = document.getElementsByClassName('nuxtDefault')
      const loggedLinks = document.getElementsByClassName('nuxtLogged')
      if (this.tok) {
        for (let i = 0; i < defaultLinks.length; i++) {
          defaultLinks[i].style.display = 'none'
        }
        for (let i = 0; i < loggedLinks.length; i++) {
          loggedLinks[i].style.display = 'flex'
        }
      } else {
        for (let i = 0; i < defaultLinks.length; i++) {
          defaultLinks[i].style.display = 'flex'
        }
        for (let i = 0; i < loggedLinks.length; i++) {
          loggedLinks[i].style.display = 'none'
        }
      }
    },
   }
</script>

Create Pages for your Nuxt app
.../logform-app
    /pages
        /logout
            index.vue
                <template>
                    <div>
                    </div>
                </template>
                <script>
                export default{
                    mounted(){
                        localStorage.clear()
                        let route = this.$router.resolve({ path: "/" });
                        window.open(route.href,"_self");
                    }
                }
                </script>
        /login
            index.vue
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
        /signup
            index.vue
                <template>
                <div class="w-full max-w-xs mx-auto">
                    <form v-on:submit.prevent="signup_cred()" class="w-full max-w-lg">
                    <div class="flex flex-wrap -mx-3 mb-6">
                        <div class="w-full md:w-1/2 px-3 mb-6 md:mb-0">
                        <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-first-name">
                            First Name
                        </label>
                        <input required class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" v-model="firstname" type="text" placeholder="name">
                        </div>
                        <div class="w-full md:w-1/2 px-3">
                        <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-last-name">
                            Last Name
                        </label>
                        <input required class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" v-model="lastname" type="text" placeholder="lastname">
                        </div>
                    </div>
                    <div class="flex flex-wrap -mx-3 mb-6">
                        <div class="w-full px-3">
                        <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-username">
                            Username
                        </label>
                        <input required class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" v-model="username" type="text" placeholder="username">
                        <!-- <p class="text-gray-600 text-xs italic">Make it as long and as crazy as you'd like</p> -->
                        </div>
                    </div>
                    <div class="flex flex-wrap -mx-3 mb-6">
                        <div class="w-full px-3">
                        <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-email">
                            Email
                        </label>
                        <input required class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" v-model="email" type="email" placeholder="email">
                        <!-- <p class="text-gray-600 text-xs italic">Make it as long and as crazy as you'd like</p> -->
                        </div>
                    </div>
                    <div class="flex flex-wrap -mx-3 mb-6">
                        <div class="w-full px-3">
                        <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-password">
                            Password
                        </label>
                        <input required class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" v-model="password" type="password" placeholder="******************">
                        <p class="text-gray-600 text-xs italic">Make it as long and as crazy as you'd like</p>
                        </div>
                    </div>
                    <div class="flex items-center justify-between">
                            <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">
                                Sign Up
                            </button>
                            <!-- <a class="inline-block align-baseline font-bold text-sm text-blue-500 hover:text-blue-800" href="#">
                                Forgot Password?
                            </a> -->
                    </div>
                    </form>
                </div>
                </template>
                <script>
                import axios from 'axios';
                let isLoggedIn = '';
                export default {
                data() {
                    return {
                    username: '',
                    password: '',
                    email: '',
                    firstname: '',
                    lastname: ''
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
                    signup_cred(event) {
                    let users_data = {
                        username: this.username,
                        password: this.password,
                        email: this.email,
                    };
                    let userlogcreds_data = {
                        firstname: this.firstname,
                        lastname: this.lastname
                    }
                    console.log(users_data);
                    // Request API.
                    axios.post('http://localhost:1337/api/auth/local/register', users_data).then(response => {
                        // Handle success.
                        console.log('Well done!');
                        console.log('User profile', response.data.user);
                        console.log('User token', response.data.jwt);
                        this.username = '';
                        this.email = '';
                        this.password= '';
                        this.firstname= '';
                        this.lastname= '';
                        const options = {
                        method: 'POST',
                        url: 'http://localhost:1337/api/user-log-creds',
                        headers: {
                            Authorization: 'Bearer ' + response.data.jwt,
                            'content-type': 'application/json'
                        },
                        data: {data: {firstname: userlogcreds_data.firstname, lastname: userlogcreds_data.lastname}}
                        };
                        axios.request(options).then(function (responsen) {
                        console.log(responsen.data);
                        window.open("http://localhost:3000/login","_self");
                        }).catch(function (error) {
                        // Handle error.
                        console.log('An error occurred:', error);
                        });
                    }).catch(error => {
                        // Handle error.
                        console.log('An error occurred:', error);
                        this.password='';
                    });  
                    }
                }
                }
                </script>
                <style scoped>
                </style>
        index.vue
            <template>
                    <div class="flex justify-center items-center">
                        <div class="text-center bg-blue-400 px-8 pt-8">
                            <h1 class="text-6xl">Welcome</h1>
                            <p class="text-xl">{{ token ? token : 'GUEST' }}</p>
                        </div>
                    </div>
            </template>
            <script>
                let token = '';
                export default {
                data() {
                    return {token}
                },
                mounted() {
                    this.token = localStorage.getItem('name')
                    console.log('Mounted: ', this.token);
                },
                }
            </script>