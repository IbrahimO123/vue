<template>
  <div>
    <div>
      <h2>Hello {{ fullName }}</h2>
      <button type="button" @click="alertFullName">Alert Fullname</button>
    </div>
    <button @click="getPost">Load Posts</button>
    <div v-if="!error">
      <div v-for="(post, index) in posts.slice(0, 10)" :key="index">
        <h3>{{ post.id }} {{ post.title }}</h3>
        <div>
          {{ post.body }}
          <hr />
        </div>
      </div>
    </div>
    <div v-else>
      <h3>Error: {{ error }}</h3>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { computed } from "vue";
export default {
  name: "PortLists",
  data() {
    return {
      posts: [],
      error: "",
    };
  },
  setup(props, context) {
    console.log("Context: ", context)
    const fullName = computed(() => `${props.firstName} ${props.lastName}`);
    function alertFullName() {
      context.emit("callFullName", fullName.value);
    }

    return { fullName, alertFullName };
  },
  props: ["firstName", "lastName"],
  methods: {
    async getPost() {
      try {
        const res = await axios.get(
          "https://jsonplaceholder.typicode.com/posts"
        );
        const data = res.data;
        this.posts = await data;
      } catch (err) {
        this.error = err.message;
        console.log("Error Message: ", err.message);
      }
    },
  },
};
</script>

<style scoped></style>
