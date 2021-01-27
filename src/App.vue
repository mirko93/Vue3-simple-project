<template>
  <div id="app">
    <nav>
      <router-link to="/">
        <div class="navigation__logo">Application</div>
      </router-link>
      

      <div class="navigation__user">
        {{ state.user.username }}
      </div>
    </nav>

    <router-view></router-view>
  
  </div>
</template>

<script>
import { reactive } from 'vue';

export default {
  name: 'App',

  setup() {
    const state = reactive({
      user: {
        username: '_johnDoe_',
      }
    });

    return {
      state
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
