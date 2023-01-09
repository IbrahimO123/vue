<template>
  <div>
    <form @submit="createPost">
      <p>
        <label for="userId">User Id:</label>
        <input type="text" id="userId" v-model="formData.userId" />
      </p>
      <p>
        <label for="title">Title:</label>
        <input type="text" id="title" v-model="formData.title" />
      </p>
      <p>
        <label for="body">Body:</label>
        <input type="text" id="body" v-model="formData.body" />
      </p>
      <p>
        <button type="submit">Submit</button>
      </p>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "CreateLists",
  data() {
    return {
      formData: {
        userId: "",
        title: "",
        body: "",
      },
    };
  },
  methods: {
    createPost(e) {
      e.preventDefault();
      axios
        .post("https://jsonplaceholder.typicode.com/posts", this.formData)
        .then((res) => console.log(res.data))
        .catch((e) => console.log(e.message));
    },
  },
};
</script>

<style scoped>
label {
  display: block;
  margin-bottom: 10px;
}
</style>
