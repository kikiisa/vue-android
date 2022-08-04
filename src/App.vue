<template>
  <router-view/>
</template>

<style>
body{
    background-color: #D1D5DB;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  font-family: 'Quicksand', sans-serif;
}

#nav {
  padding: 30px;
}

.primary-bg{background-color: #374151;}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
