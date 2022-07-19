<template>
  <div id="app">
    <div class="container">
      <add-bar @addToDo="addToDo" ></add-bar>
      <to-do
          style="margin-right: auto;margin-left: auto;"
          :todos="todos"
      ></to-do>
    </div>
  </div>
</template>

<script>

import ToDo from "@/components/ToDoList";
import AddBar from "@/components/AddBar";

export default {
  name: 'App',
  components:{
    ToDo,
    AddBar
  },
  data() {
    return {
      todoStatus: ["Выполнено", "В работе"],
      columns: ['name', 'status', 'date'],
      todos: [
        {
          name: "Размещение новостей на сайте",
          status: "Выполнено",
          date: "2022-04-22",
        },
        {
          name: "Внедрить Wi-fi для читателей",
          status: "В работе",
          date: "2022-03-25",
        },
        {
          name: "Отредактировать раздел “Доступная среда”",
          status: "Выполнено",
          date: "2022-03-15"
        },
        {
          name: "Презентация “Информационные технологии”",
          status: "В работе",
          date: "2022-03-15"
        },
        {
          name: "Счётчики — внедрить дизайн",
          status: "В работе",
          date: "2022-03-09"
        },
        {
          name: "Сверстать новый layout",
          status: "В работе",
          date: "2022-03-07"
        },
        {
          name: "Скролл в новостях",
          status: "Выполнено",
          date: "2022-03-01"
        },
        {
          name: "Форма сброса пароля",
          status: "В работе",
          date: "2022-02-25"
        },
        {
          name: "Внедрение модуля Chat",
          status: "Выполнено",
          date: "2022-02-20"
        },
      ],
    }
  },
  mounted() {
    if (localStorage.getItem('todos')) {
      try {
        this.todos = JSON.parse(localStorage.getItem('todos'));
      } catch(e) {
        localStorage.removeItem('todos');
      }
    }
  },
  methods: {
    addToDo(newToDo) {
      let yourDate = new Date();
      this.todos.push({name: newToDo, status: 'В работе', date: yourDate.toISOString().split('T')[0]})
      this.saveToDo();
    },
    saveToDo() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem('todos', parsed);
    }
  }
}
</script>

<style>
@font-face {
  font-family: "Montserrat-Bold";
  font-style: normal;
  src: url("assets/Montserrat-Bold.ttf")
}
.container{
  margin:8%;
}
h2{
  font-family: Montserrat-Bold, normal;
  font-size: 24px;
}
</style>
