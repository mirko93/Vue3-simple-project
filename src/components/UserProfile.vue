<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>

      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>

      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>

      <form action="" class="user-profile__create-post" @submit.prevent="createNewPost">
        <label for="newPost">
          <strong>New Post</strong>
        </label>
        <textarea id="newPost" rows="4" placeholder="Type the text" v-model="newPostContent"></textarea>

        <div class="user-profile__create-post-type">
          <label for="newPostType">
            <strong>Type: </strong>
          </label>

          <select id="newPostType" v-model="selectedPostType">
            <option :value="option.value" v-for="(option, index) in postTypes" :key="index">
              {{ option.name }}
            </option>
          </select>

        </div>

        <button>Post!</button>
      </form>
    </div>

    <div class="user-profile__post-wrapper">
      <PostItem 
        v-for="post in user.posts" 
        :key="post.id" 
        :username="user.username" 
        :post="post" 
        @favourite="toggleFavourite" 
      />
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
      newPostContent: '',
      selectedPostType: 'instant',
      postTypes: [
        { value: 'draft', name: 'Draft' },
        { value: 'instant', name: 'Instant Post' }
      ],
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
    },

    createNewPost() {
      if (this.newPostContent && this.selectedPostType !== 'draft') {
        this.user.posts.unshift({
          id: this.user.posts.length + 1,
          content: this.newPostContent,
        });

        this.newPostContent = '';
      }
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
  margin: 5px;
}

h1 {
  margin: 0;
}

.user-profile__post-wrapper {
  display: grid;
  grid-gap: 10px;
}

.user-profile__create-post {
  display: flex;
  flex-direction: column;
  border-top: 1px solid black;
  padding-top: 10px;
}
</style>
