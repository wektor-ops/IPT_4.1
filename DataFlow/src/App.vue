<script  setup lang="ts">
import { faker } from '@faker-js/faker'
import { ref } from 'vue'
import Post from './components/Post.vue'

const unSortedposts = ref([
  { id: 1, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 8 },
  { id: 2, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 0 },
  { id: 3, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: -4 },
  { id: 4, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 0 },
  { id: 5, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: -8 },
  { id: 6, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 4 },
  { id: 7, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 6 },
  { id: 8, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 3 },
  { id: 9, title: faker.lorem.words(10), text: faker.lorem.paragraph(), user: faker.internet.userName(), votes: 15 },
])
const posts = computed(() =>
    [...unSortedPosts.value].sort((a, b) => b.votes - a.votes)
);
function voteUp (newid) {
  console.log('voteUp', newid)
  const post = posts.value.find(post => post.id === newid)
  post.votes++;
}

function voteDown (newid) {
  console.log('voteDown', newid)
  const post = posts.value.find(post => post.id === newid)
  post.votes--;
}
</script>

<template>
  <div class="container" >
    <Post v-for="post in posts" :key="post.id"
        :id="post.id"
        :title="post.title"
        :text="post.text"
        :user="post.user"
        :votes="post.votes"
          @voteUp="voteUp($event)"
          @voteDown="voteDown($event)"
    />
  </div>

</template>

<style>
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
  font-size: 16px;
  background: #f0f0f0;
}

.container {
  max-width: 800px;
  margin: 40px auto;
  border: 1px solid #fafafa;
  box-shadow: 0 0 2px rgba(0, 0, 0, .2);
  background: #fff;
  border-radius: 4px;
  position: relative;
}
</style>