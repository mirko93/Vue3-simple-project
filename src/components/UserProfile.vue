<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>

      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>

      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
    </div>

    <div class="user-profile__posts-wrapper">
      <PostItem v-for="post in user.posts" :key="post.id" :username="user.username" :post="post" @favourite="toggleFavourite" />
    </div>
  </div>
</template>

<script>
import PostItem from './PostItem';

export default {
  name: 'UserProfile',

  components: {
    PostItem,
  },

  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: '_johnDoe_',
        firstName: 'John',
        lastName: 'Doe',
        email: 'johndoe@email.com',
        isAdmin: true,
        posts: [
          { id: 1, content: 'New Post Amazing!' },
          { id: 2, content: "Don't forget is subscribe." },
        ]
      }
    }
  },

  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`);
      }
    }
  },

  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },

  methods: {
    followUser() {
      this.followers++;
    },

    toggleFavourite(id) {
      console.log(`Favourited Post #${id}`);
    }
  },

  mounted() {
    this.followUser();
  }
}
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #DFE3E8;
}

.user-profile__admin-badge {
  background-color: tomato;
  color: #fff;
  font-weight: bold;
  text-align: center;
}
</style>
