<template>
  <div class="row">
    <h2 style="width: 70%">To do list</h2>
    <img
        src="../assets/addToDo.png"
        style="width: 40px; height: 40px;"
        @click="showModal=true"
    >
      <div v-if="showModal" class="modal-mask">
        <div class="modal-wrapper">
          <div class="modal-container">

            <div class="modal-header">
              <slot name="header" class="header">
                <b>Создать новую задачу</b>
              </slot>
              <img src="../assets/close.png" @click="showModal=false">
            </div>

            <div class="modal-body">
              <slot name="body">
                <p style="margin: 0">Описание</p>
                <input style="width: 100%; border-color: white" v-model="newToDo" placeholder="Введите описание">
              </slot>
            </div>

            <div class="modal-footer">
              <slot name="footer">
                <button class="modal-default-button" @click="addToDo()">
                  Создать
                </button>
              </slot>
            </div>
          </div>
        </div>
      </div>
  </div>
</template>

<script>

export default {
  name: "AddBar",
  components: {

  },
  data(){
    return{
      showModal: false,
      newToDo: null
    }
  },
  methods: {
    addToDo() {
      this.$emit('addToDo', this.newToDo);
      this.showModal = false;
    }
  }
}
</script>

<style scoped>
.header{
  float: right;
}
img{
  height: 22px;
  width: 22px;
  float: right;
}
@font-face {
  font-family: "VelaSans";
  font-style: normal;
  src: url("../assets/VelaSans-Regular.otf")
}
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
  padding: 40px;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 40px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  font-family: VelaSans;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
  font-size: 14px;
}

.modal-default-button {
  color: #314B99;
  background-color: #F0F5FF;
  border-color: white;
  font-size: 18px;
  position: relative;
  left: 50%;
  transform: translate(-50%, 0);
}
.row{
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
}
img{
  display: block;
  margin: auto auto auto 20%;
}
</style>