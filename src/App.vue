<template>
  <div id="app">
    <nav>
      <div class="navigation__logo">
        Application
      </div>

      <div class="navigation__user">
        {{ user.username }}
      </div>
    </nav>
    <UserProfile />
  </div>
</template>

<script>
import UserProfile from './components/UserProfile.vue'

export default {
  name: 'App',

  components: {
    UserProfile,
  },

  data() {
    return {
      user: {
        username: '_johnDoe_',
      }
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Times New Roman', Times, serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #F3F5FA;

  nav {
    display: flex;
    justify-content: space-between;
    background-color: sandybrown;
    padding: 20px;
  }
}
</style>
