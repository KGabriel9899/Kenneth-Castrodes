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
let frun = false;
export default {
  data() {
    return {token,frun}
  },
  mounted() {
    // if(!this.frun){
    //   localStorage.clear();
    //   console.log("frun " + this.frun);
    //   this.frun = true;
    //   console.log("frun " + this.frun);
    // }
    this.token = localStorage.getItem('name')
    console.log('Mounted: ', this.token);
  },
}
</script>
<style scoped>
</style>