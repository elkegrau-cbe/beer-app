<template>
  <nav>
    <router-link to="/">Home</router-link> &nbsp;&nbsp;|&nbsp;&nbsp;
    <router-link to="/about">About</router-link>
  </nav>
  <router-view />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 20px;
}

nav a {
  font-weight: bold;
  color: #746a5d;
}

nav a.router-link-exact-active {
  color: #be8323;
}
</style>
