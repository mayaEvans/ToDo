<template>
  <div>
    <div style="margin-bottom: 20px; margin-top: 10px;">
      <div style="display: inline-block;">
        <img style="float: left" src="../assets/search.png">
        <input
            style="width: 270px;"
            placeholder="Поиск ID, Имени, статуса или даты"
            type="text"
            v-model="name"
            class="search-field text"
        >
      </div>
    </div>
    <div class="row">
      <div class="col-1" style="width: 6%; "></div>
      <hr color="#C4C4C4">
      <div class="col-7 text">Описание</div>
      <hr color="#C4C4C4">
      <div class="col-2 text">Статус</div>
      <hr color="#C4C4C4">
      <div class="col-2 text">Дата</div>
    </div>
    <div v-for="(todo, index) in filteredList"
         :key="index"

    >
      <div class="row">
        <div class="col-1">
          <img v-if="todo.status === 'Выполнено'" src="../assets/doneIcon.png" @click="todo.status='В работе'">
          <img v-else src="../assets/inProcessIcon.png" style="width: 20px; height: 20px;"
               @click="todo.status='Выполнено'">
        </div>
        <div class="text col-7">
          {{ todo.name }}
        </div>
        <div class="text col-2"
             :class="{
                'status-done': todo.status === 'Выполнено',
                'status-in-work': todo.status === 'В работе',
              }"
        >{{ todo.status }}
        </div>
        <div class="text col-2">{{ todo.date }}</div>
      </div>
      <hr color="#EEEBE9">
    </div>
  </div>
</template>

<script>
export default {
  name: "ToDo",
  props: ['todos'],
  data() {
    return {
      name: '',
      todoStatus: ["Выполнено", "В работе"],
    }
  },
  computed: {
    filteredList: function () {
      var nameToDo = this.name;
      return this.todos.filter(function (elem) {
        if (nameToDo === '') return true;
        else return elem.name.indexOf(nameToDo) > -1;
      })
    }
  }
}
</script>

<style scoped>
@font-face {
  font-family: "VelaSans";
  font-style: normal;
  src: url("../assets/VelaSans-Regular.otf")
}

img {
  display: block;
  margin: 0 auto;
}

.col-1 {
  padding: 20px;
  width: 6%;
}

.col-2 {
  padding: 20px;
  text-align: left;
  width: 12%;
}

.col-7 {
  padding: 20px;
  text-align: left;
  width: 70%;
}

.row {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
}

.text {
  font-family: "VelaSans", normal;
  font-size: 14px;
}

.status-done {
  color: #134EC1;
}

.status-in-work {
  color: #F89B11;
}
</style>