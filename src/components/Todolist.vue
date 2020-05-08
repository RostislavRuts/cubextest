<!--Это компонент. Он может состоять только из шаблона template.
    Единственное требование у него должен быть корневой елемент(обычно это <div>).
    что б воспользоваться этим компонентом мы должны его импортировать и зарегестрировать в App.vue-->
<template>
  <div class="container">
    <ul>
      <!--<Todotitem/> - это компонент представлен в файле Todoitem.vue
                 Там находятся наши <li>. Для передачи данных из компонента Todolist
                 воспульзуемся след. директивами фреймворка:

                 1. v-for - цикл разберет наш массив(см.27) на отдельные ел-ты

                 2. v-bind - создает атрибуты в ел-тах.
                    Эти атрибуты кроме строковых значений могут принимать массивы или объекты.
                    v-bind:class=" ", class - название аттрибута(именно название класса мы предаем компоненту Todoitem.vue).
                    В нашем случаи значение класса это ел-ты массива itemsfortodos

                 3. v-on - Это событие было создано в компоненте Todoitem,
                    оно будет удалять ел-ты основного списка.
      removeListItem - метод-->
      <Todoitem
        v-for="(item, index) of itemsfortodos"
        v-bind:todo="item"
        v-bind:id="index"
        v-on:remove-list="removeItem"
        @add-sub-list="addSubList"
      />

      <AddNewList @add-main-list="addList"/>
    </ul>
  </div>
</template>

<script>
import Todoitem from "@/components/Todoitem";
import AddNewList from "@/components/AddNewList";
export default {
  /*Для того что бы компонент знал что мы ему что-то передаем
         в этом объекте создаем поле props в массиве которого указываем каждый елемент
         который передаем, в нашем случаи это itemsfortodos
         Передача  массива происходит с файла App.vue*/
  props: ["itemsfortodos"],
  components: {
    /*Это обьект в котором мы регистрируем компонент(которым будем управлять) по принципу
     *ключ: значение(Todolist:Todolist), но если это одно и тоже можно указать название Todolist */
    Todoitem,
    AddNewList
  },
  methods: {
    removeItem(id) {
      //console.log(id)
      this.$emit("remove-list", id);
    },

    addList(newList) {
      //console.log(newList);
      this.$emit('add-list', newList)
    },

    addSubList(newSubList){
      this.$emit('add-sub-list', newSubList)
      //console.log(newSubList)
    }
  }
};
</script>

<!--scoped - локализирунт стили.
    Теперь прописанные ниже стили работают только для этого компонента-->
<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>