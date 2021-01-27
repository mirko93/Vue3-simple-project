<template>
  <form
    class="user-profile__create-post"
    @submit.prevent="createNewPost"
    :class="{ '--exceeded': newPostCharacterCount > 100 }"
  >
    <label for="newPost">
      <strong>New Post</strong>
      ({{ newPostCharacterCount }}/100)
    </label>
    <textarea
      id="newPost"
      rows="4"
      placeholder="Type the text"
      v-model="state.newPostContent"
    ></textarea>

    <div class="user-profile__create-post-type">
      <label for="newPostType">
        <strong>Type: </strong>
      </label>

      <select id="newPostType" v-model="state.selectedPostType">
        <option
          :value="option.value"
          v-for="(option, index) in state.postTypes"
          :key="index"
        >
          {{ option.name }}
        </option>
      </select>
    </div>

    <button>Post!</button>
  </form>
</template>

<script>
import { reactive, computed } from 'vue';

export default {
    name: 'CreatePostPanel',

    setup(props, ctx) {
        const state = reactive({
            newPostContent: '',
            selectedPostType: 'instant',
            postTypes: [
                { value: 'draft', name: 'Draft' },
                { value: 'instant', name: 'Instant Post' }
            ],
        });

        const newPostCharacterCount = computed(() => state.newPostContent.length);

        function createNewPost() {
            if (state.newPostContent && state.selectedPostType !== "draft") {
                ctx.emit('add-post', state.newPostContent);
                state.newPostContent = '';
            }
        }

        return {
            state,
            newPostCharacterCount,
            createNewPost
        }
    },
};
</script>

<style>
</style>