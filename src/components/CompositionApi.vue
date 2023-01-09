<template>
  <div>
    <h3>Options Api: {{ o_firstname }}</h3>
    <h3>Composition Api: {{ c_firstname }}</h3>
    <h4>{{ greetPerson }}</h4>
    <div>
      <h3>{{ profile.title }}</h3>
      <h5>{{ profile.version }}: {{ profile.genre }}</h5>
      <div v-for="(topic, index) in profile.keywords" :key="index">
        <h6>{{ topic }}</h6>
      </div>
    </div>
    <div>
      <h6>Mathematics Score: {{ Mathematics }}</h6>
      <h6>English Score: {{ English }}</h6>
      <h6>Computer Science: {{ Computer_Science }}</h6>
      <button @click="changeResults">Change results</button>
    </div>
  </div>
</template>

<script>
import { ref, reactive, toRefs } from "vue";
export default {
  name: "CompositionApi",
  data() {
    return {
      o_firstname: "Ibrahim",
    };
  },
  setup() {
    const c_firstname = ref("");
    c_firstname.value = "Kolawole";
    const c_fullname = reactive({
      firstname: "Ibrahim",
      lastname: "Oliyide",
      othername: "Kolawole",
    });
    const greetPerson = `Good Morning ${c_fullname.firstname} ${c_fullname.lastname} ${c_fullname.othername}`;
    const profile = reactive({
      title: "Software Engineer",
      version: "1.0.0",
      genre: "Action",
      keywords: ["Vue", "Javascript", "Typescript"],
    });
    const results = reactive({
      Mathematics: 78,
      English: 90,
      Physics: 80,
      Computer_Science: 50,
    });
    const changeResults = () => {
      results.Mathematics = 100;
      results.English = 100;
      results.Physics = 100;
      results.Computer_Science = 100;
    };
    return {
      c_firstname,
      greetPerson,
      profile,
      ...toRefs(results),
      changeResults,
    };
  },
};
</script>

<style scoped></style>
