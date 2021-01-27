<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ state.user.username }}</h1>

      <h3>{{ userId }}</h3>

      <div class="user-profile__admin-badge" v-if="state.user.isAdmin">Admin</div>

      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ state.followers }}
      </div>

      <CreatePostPanel @add-post="addPost" />
    </div>

    <div class="user-profile__post-wrapper">
      <PostItem 
        v-for="post in state.user.posts" 
        :key="post.id" 
        :username="state.user.username" 
        :post="post"  
      />
    </div>
  </div>
</template>

<script>
import { reactive, computed } from 'vue';
import { useRoute } from 'vue-router';
import { users } from '../assets/users';
import PostItem from '../components/PostItem';
import CreatePostPanel from '../components/CreatePostPanel';

export default {
  name: 'UserProfile',

  components: {
    PostItem,
    CreatePostPanel,
  },

  setup() {
    const route = useRoute();
    const userId = computed(() => route.params.userId);

    const state = reactive({
      followers: 0,
      user: users[userId.value - 1] || users[0],
    });

    function addPost(post) {
      state.user.posts.unshift({
        id: state.user.posts.length + 1,
        content: post
      });
    }

    return {
      state,
      addPost,
      userId
    }
  },
}
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;

  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;

    h1 {
      margin: 0;
    }

    .user-profile__admin-badge {
      background-color: tomato;
      color: #fff;
      font-weight: bold;
      text-align: center;
      margin: 5px;
    }

    .user-profile__create-post {
      display: flex;
      flex-direction: column;
      border-top: 1px solid black;
      padding-top: 10px;

      &.--exceeded {
        color: red;
        border-color: red;
      }
    }
  }

  .user-profile__post-wrapper {
    display: grid;
    grid-gap: 10px;
  }
}


</style>
