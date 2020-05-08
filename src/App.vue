<template>
  <div id="app">
    <h1>User application</h1>
    <h3>Create your notes quickly and easily</h3>
    <hr>
    <!--<Todolist/> - это компонент представлен в файле Todolist.vue
         Vue предоставляет дополнительные возможности директивы v-bind для работы с class и style.
         Эти атрибуты кроме строковых значений могут принимать массивы или объекты.
         v-bind:class=" ", class - название аттрибута(именно название класса мы предаем компоненту Todolist.vue).
         В нашем случаи значение класса это массив todos см.40

         @remove-list="removeListItem" - один из способов вызвать событие вместо v-on.
    Это событие для удаления ел-та списка(см.24 в файле Todolist.vue)-->
    <Todolist
      v-bind:itemsfortodos="todos"
      @remove-list="removeItem"
      @add-list="addList"
      @add-sub-list="addSubList"
    />
  </div>
</template>
<!--
2. Секция скрипт в которую мы импортим какой-то объект(она представляет весь функционал данного файла)-->
<script>
/*
 * Ниже импортим компонент Todolist.
 * @ - ссылается на папку src*/
import Todolist from "@/components/Todolist";

export default {
  name: "App",
  /*Для работы с данными компонента создаем фукцию data()*/
  data() {
    return {
      /*Массив todos содержит в себе данные, которые мы передаем в компонент Todolist.
       * Для этого будем использовать v-bind в секции(шаблоне) Todolist этого файла*/
      todos: []
    };
  },
  /*Это обьект в котором мы регистрируем компонент(которым будем управлять) по принципу
   *ключ: значение(Todolist:Todolist), но если это одно и тоже можно указать название Todolist */
  components: {
    Todolist
  },
  methods: {
    /*removeListItem(id) - метод для удаления ел-тов списка. Он будет выполняться
     * в момент вызова события "remove-list" созданного в компоненте Todoitem(см.17),
     * id - параметр (id елемента по которому кликаем), полученный из этого же события.
     * Те же действия мы должны повторить в App.vue*/

    removeItem(id) {
      this.todos = this.todos.filter(function(el, index) {
        return index + 1 !== id;
      });
    },
    addList(newList) {
      this.todos.push(newList);
      //console.log(this.todos)
    },
    addSubList(newSubList) {
      let parent = this.todos.findIndex(function(el, index) {
        return index == newSubList.id;
      });
      //console.log(parent, newSubList.id, this.todos[parent].sublist);
      delete newSubList.id;
      this.todos[parent].sublist.push(newSubList);
      //console.log(this.todos)
    }
  }
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
</style>