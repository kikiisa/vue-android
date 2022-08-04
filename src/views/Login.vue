<template>
    <Navbar/>
    <div class="container">
        <Login/>
    </div>
</template>
<script>
import Navbar from "@/components/Navbar.vue";
import Login from "@/components/LoginComponent.vue";
export default {
  name: "Home",
  components: {
    Navbar,Login
  },
};
</script>
<style scoped>
    .container{
        margin-top:40px;
    }
</style>
