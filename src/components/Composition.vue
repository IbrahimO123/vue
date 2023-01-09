<template>
  <div>
    <div>
      <h5>{{ count }}</h5>
      <p>
        <button @click="increment">+</button>
        <button @click="decrement">-</button>
      </p>
    </div>
    <div>
        <h6>Inject Api using Composition Api {{ childUserName }}</h6>
    </div>
    <p>Option Api</p>
    <input placeholder="First Name" v-model="fName" />
    <input placeholder="Lirst Name" v-model="lName" />
    <p>Composition Api</p>
    <input placeholder="First Name" v-model="firstName" />
    <input placeholder="Last Name" v-model="lastName" />
    <p>Reactive state</p>
    <input placeholder="Age" v-model="age" />
    <input placeholder="Student Name" v-model="studentName" />
    <input placeholder="Best Subject" v-model="bestSubject" />
    <h3>Composition, Full name is {{ fullName }}</h3>
    <h3>Composition, Student Details are {{ studentDetails }}</h3>
    <div>
      <h2>Email</h2>
      <h6>{{ from }}</h6>
      <label>To:</label>
      <input type="email" placeholder="to" v-model="to" />
      <label>Subject:</label>
      <input type="text" placeholder="Subject" v-model="subject" />
      <label for="body">Message:</label>
      <textarea
        type="text"
        id="body"
        placeholder="Write your mail"
        v-model="body"
      ></textarea>
    </div>
  </div>
</template>

<script>
import { ref, reactive, toRefs, computed, watch, inject } from "vue";
export default {
  name: "CompositionApi",
  data() {
    return {
      fName: "",
      lName: "",
    };
  },
  setup() {
    const firstName = ref("");
    const lastName = ref("");
    const count = ref(0);
    const increment = () => {
      return count.value++;
    };
   
    const decrement = () => {
      if (count.value <= 0) return (count.value = 0);
      return count.value--;
    };
    const state = reactive({
      age: 0,
      studentName: "Oliyide Ismail",
      bestSubject: "Mathematics",
      subjects: ["Mathematics", "English", "Physics", "Chemistry", "Biology"],
    });
    const fullName = computed(() => {
      return `${firstName.value} ${lastName.value}`;
    });
    const studentDetails = computed(() => {
      return `${state.age} ${state.studentName} ${state.bestSubject}`;
    });

    const readingBook = ref("");
    const shop = ref("");
    const client = watch([shop, readingBook], (newValue, oldValue) => {
      console.log("New Value: ", newValue[0]);
      console.log("Old Value: ", oldValue[0]);
      console.log("New Value: ", newValue[1]);
      console.log("Old Value: ", oldValue[1]);
    });

    const mail = reactive({
      from: "Oliyide Ibrahim",
      to: "",
      subject: "",
      body: "",
    });

     const childUserName = inject("c_username", "Default Username")
    return {
      firstName,
      childUserName,
      lastName,
      ...toRefs(state),
      fullName,
      studentDetails,
      readingBook,
      shop,
      client,
      ...toRefs(mail),
      count,
      increment,
      decrement,
    };
  },
};
</script>

<style scoped>
/* input {
  display: block;
  width: 70px;
  margin: 5px;
} */
/* label{
    display:
} */
/* textarea {
    display: block;
} */
button {
  margin: 5px;
}
input {
  margin: 5px;
}
</style>
