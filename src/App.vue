<template>
  <button class="text-end m-1 btn btn-secondary" @click="Logout">Odjava</button>
  <router-view/>
</template>

<script>
export default {
  data() {
    return {
      title: ''
    };
  },
  methods: {
    Logout() {
      this.$router.push({ name: 'Home' })
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
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
