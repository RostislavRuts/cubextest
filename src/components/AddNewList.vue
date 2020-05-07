<!--Этот компонент - форма для добавления новых ел-тов основного списка-->
<template>
  <form @submit.prevent="addList">
    <input type="text" v-model="title" placeholder="Enter note title">
    <button type="submit">Add New List</button>
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
    addList() {
      //console.log("submit", this.title);
      if (this.title.trim()) {
        const newList = {
          title: this.title,
          completed: false,
          sublist: []
        };
        this.$emit("add-main-list", newList);
        this.title = "";
      }
    }
  }
};
</script>

<style>
form {
  width: 50%;
  display: flex;
  justify-content: space-between;
}
input {
  width: 50%;
}
</style>