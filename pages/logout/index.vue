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