<!--Это компонент. Он может состоять только из шаблона template.
    Единственное требование у него должен быть корневой елемент(обычно это <div>), но в нашем
    случаи это <li>. Потому как этот компонент взаимодействует с другим Todolist.vue(в нем уже ессть нужная верстка )
    что б воспользоваться этим компонентом мы должны его импортировать и зарегестрировать в App.vue-->
<template>
  <li>
    <span>
      <b>{{todo.title}}</b>
    </span>

    <AddSubList/>

    <!--v-on - добавляет событие к елементу
        $emit(1й параметр - название события, 2й - какие-то передаваемые данные) - создает события
    Елемент Todoitem дочерний у компонента Todolist поэтому он должен получить это событие-->
    <button class="rm" v-on:click="$emit('remove-list', id + 1)">&times;</button>
  </li>
</template>

<script>
import AddSubList from "@/components/AddSublist";
export default {
  /* Для того что бы компонент знал что мы ему что-то передаем
          в этом объекте создаем поле(метод) props в массиве которого указываем каждый елемент
          который передаем c помощью директивы v-bind). Передача  массива происходит с файла Todolist.vue*/
  props: {
    todo: {
      /*Сейчас сделали валидацию входящих данных.
       * указали название входящего свойства
       * далее валидируем тип входящих данных объект
       * и говорим что если его нет то не выводим*/
      type: Object,
      required: true
    },
    id: Number
  },
  components: {
    AddSubList
  }
};
</script>

<style scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 2rem;
  margin-bottom: 1rem;
  width: 50%;
}
.rm {
  background: red;
  color: #fff;
  border-radius: 50%;
  font-weight: bold;
}
</style>