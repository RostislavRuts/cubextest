<template>
  <form @submit.prevent="addSubList">
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
      if (this.title.trim()) {
        const newSubList = {
          title: this.title,
          completed: false,
          sublist: []
        };
        this.$emit("add-sub-list", newSubList);
        this.title = "";
      }
    }
  }
};
</script>