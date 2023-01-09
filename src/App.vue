<template>
  <div>
    <input type="text" ref="inputRef" v-model="channel" />
    <input type="text" placeholder="First Name" v-model="firstName" />
    <input type="text" placeholder="Last Name" v-model="lastName" />
    <PortLists
      :firstName="firstName"
      :lastName="lastName"
      @callFullName="callFullName"
    />
    <p>
      <CreateLists />
    </p>
    <div>
      <CompositionApi />
    </div>
  </div>
</template>

<script>
import PortLists from "./components/PortLists.vue";
import CreateLists from "./components/CreateLists.vue";
import CompositionApi from "./components/Composition.vue";
import { provide, ref, onMounted } from "vue";

export default {
  name: "App",
  components: {
    PortLists,
    CreateLists,
    CompositionApi,
  },

  setup() {
    const inputRef = ref(null);
    onMounted(() => {
      inputRef.value.focus();
    });
    const callFullName = (fullName) => {
      alert("Alert of the User fullname " + fullName);
    };
    const channel = ref(" ");
    const firstName = ref(" ");
    const lastName = ref(" ");
    provide("c_username", channel);
    return { channel, inputRef, firstName, lastName, callFullName };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
label {
  display: block;
  margin-bottom: 10px;
}
</style>
