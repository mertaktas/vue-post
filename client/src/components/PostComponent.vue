<template>
  <div class="container">
    <h1>Post App</h1>
    <div class="create-post">
      <label for="create-post">Birşeyler yaz</label>
      <input type="text" id="create-post" v-model="text" v-bind:placeholder="value" />
      <button v-on:click="createPost">Post!</button>
    </div>
    <hr />
    <p class="error" v-if="error">{{ error }}</p>
    <div class="posts-container">
      <div
        class="post"
        v-for="(post, index) in posts"
        v-bind:item="post"
        v-bind:index="index"
        v-bind:key="post._id"
      >
        <h6 class="date">
          {{
          `${post.createdAt.getDate()}/${post.createdAt.getMonth()}/${post.createdAt.getFullYear()}`
          }}
        </h6>
        <p class="text">{{ post.text.substring(0, 100) }}..</p>
        <button class="btn" v-on:click="deletePost(post._id)">DltPost!</button>
      </div>
    </div>
  </div>
</template>

<script>
import PostService from "../PostServices";

export default {
  name: "PostComponent",
  data() {
    return {
      posts: [],
      error: "",
      text: "",
      value: "Buraya birşey yazın"
    };
  },
  async created() {
    try {
      this.posts = await PostService.getPosts();
    } catch (err) {
      this.error = err.message;
    }
  },
  methods: {
    async createPost() {
      await PostService.insertPost(this.text);
      this.posts = await PostService.getPosts();
      setTimeout((this.text = ""), 1000);
    },
    async deletePost(id) {
      await PostService.deletePost(id);
      this.posts = await PostService.getPosts();
    }
  }
};
</script>

<style scoped>
div.container {
  max-width: 800px;
  margin: 0 auto;
}

p.error {
  border: 1px solid #ff5b5f;
  background-color: #ffc5c1;
  padding: 10px;
  margin-bottom: 15px;
}

div.post {
  position: relative;
  border: 1px solid #5bd658;
  background-color: #bcffb8;
  padding: 10px 10px 30px 10px;
  margin-bottom: 15px;
}

div.created-at {
  position: absolute;
  top: 0;
  left: 0;
  padding: 5px 15px 5px 15px;
  background-color: darkgreen;
  color: white;
  font-size: 13px;
}

p.text {
  font-size: 22px;
  font-weight: 200;
  margin-bottom: 0;
}
h6.date {
  float: right;
}
</style>
