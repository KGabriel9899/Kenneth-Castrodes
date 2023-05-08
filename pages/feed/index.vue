<template>
    <section class="dark:bg-gray-800 dark:text-gray-100">
        <div class="container max-w-6xl p-6 mx-auto space-y-6 sm:space-y-12">
            <a rel="noopener noreferrer" class="block max-w-sm gap-3 mx-auto sm:max-w-full group hover:no-underline focus:no-underline lg:grid lg:grid-cols-12 dark:bg-gray-900">
                <div class="p-6 space-y-2 lg:col-span-5">
                    <h3 class="text-2xl font-semibold sm:text-4xl group-hover:underline group-focus:underline">{{ name }}</h3>
                    <span class="text-xs dark:text-gray-400">February 19, 2021</span>
                    <p>Ei delenit sensibus liberavisse pri. Quod suscipit no nam. Est in graece fuisset, eos affert putent doctus id.</p>
                </div>
            </a>
        </div>
    </section>
</template>
<script>
let isLoggedIn = '';
export default{
    data(){
        return{
            name: this.name
        }
    },
    mounted(){
        isLoggedIn = localStorage.getItem('jwt_token')
        this.name = localStorage.getItem('name');
        if (!isLoggedIn) {
            console.log("FEED");
            let route = this.$router.resolve({ path: "/" });
            window.open(route.href,"_self");
        }
    }
}
</script>
<style scoped>
</style>