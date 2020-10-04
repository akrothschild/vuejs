<template>
  <div id="app">
    {{ user.username }}
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    followers: 0,
    User: {
      id: 1,
      username: '_RichardWindsor',
      firstName: 'Richard',
      lastName: 'Windsor',
      email: 'rw@pm.me',
      isAdmin: true,
      }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
