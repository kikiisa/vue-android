<template>
    <Navbar />
    <div class="container">
        <Menu/>
    </div>
</template>
<script>
import Navbar from "@/components/Navbar.vue";
import Menu from "@/components/Menu.vue";

export default {
  name: "Home",
  components: {
    Navbar,Menu
  },
};
</script>
