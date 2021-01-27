<template>
  <div class="home">
    <h1>Home</h1>

    <div class="user-list">
      <router-link v-for="user in users" :to="{ name: 'UserProfile', params: { userId: user.id } }" :key="user.id" >
        @{{ user.username }}
      </router-link>
    </div>

  </div>
</template>

<script>
import { users } from '../assets/users'

export default {
  name: 'Home',

  setup() {
    return {
      users
    }
  }
}
</script>

<style lang="scss" scoped>
.home {
  padding: 30px 3%;

  .user-list {
    display: flex;
    flex-direction: column;

    a {
      margin-top: 10px;
      text-decoration: none;
      background-color: burlywood;
      font-weight: bold;
    }
  }
}
</style>
