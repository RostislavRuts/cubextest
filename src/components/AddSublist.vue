<template>
  <form @submit.prevent="addSubList">
    <p>{{ this.title }}</p>
    <input type="text" v-model="title" placeholder="sublist">
    <button type="submit">Add sublist</button>
  </form>
</template>


<script>
export default {
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addSubList() {
      console.log("submit", this.title);
    }
  }
};
</script>