<!-- <template>
    <div>
        <header class="shadow-sm bg-white">
            <nav class="container mx-auto p-4 flex justify-end">
                <ul class="flex gap-4">
                    <li><NuxtLink to="/">Home</NuxtLink></li>
                    <li class="nuxtLogged"><NuxtLink to="/login">Log out</NuxtLink></li>
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
let emp = '';
let tok = '';
export default {
    mounted(){
        this.tok = localStorage.getItem('name')
        if(this.tok){
            document.getElementsByClassName("nuxtDefault").style.display= "none";
            document.getElementsByClassName("nuxtLogged").style.display= "flex";
        }   
        else{
            document.getElementsByClassName("nuxtDefault").style.display= "flex";
            document.getElementsByClassName("nuxtLogged").style.display= "none";
        }  
    }
}
</script> -->

<template>
  <div>
    <header class="shadow-sm bg-white">
      <nav class="container mx-auto p-4 flex justify-end">
        <ul class="flex gap-4">
          <li><NuxtLink to="/">Home</NuxtLink></li>
          <li class="nuxtLogged"><NuxtLink to="/feed">Feed</NuxtLink></li>
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
  // beforeRouteLeave(to, from, next) {
  //     const isLoggedIn = localStorage.getItem('jwt_token')

  //     if (isLoggedIn) {
  //     // Proceed to the requested route
  //     next(false)
  //     } 
  //     else {
  //     // Redirect to login page
  //     next({ name: 'index' })
  //     }
  // }
</script>