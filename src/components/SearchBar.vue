<template>
<div>
  <div>
    <div style="display: inline-block;" >
      <img style="float: left" src="../assets/search.png">
      <input
          style="width: 270px;"
          placeholder="Поиск ID, Имени, статуса или даты"
          type="text"
          v-model="name"
          class="search-field text"
      >
    </div>
    <div class="text" style="display: inline-block; margin: auto auto auto 51%">
      <span>Сортировать по: </span>
      <select v-model="selected">
        <option>дате</option>
        <option>статусу</option>
      </select>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: "SearchBar",
  props: ['todos'],
  computed:{
  filteredList: function(){
    var comp = this.name;
    return this.name.filter(function (elem) {

      if(comp==='') return true;
      else return elem.name.indexOf(comp) > -1;
    })
  }
}
}
</script>

<style scoped>
input{
  border-color: white;
}
img{
  height: 18px;
  width: 18px;
  margin: 16px;
  margin-right: 0;
}
.search-field{
  width: 66%;
  margin: 16px;
  border-color: white;

}
.text{
  font-family: "VelaSans",normal;
  font-size: 14px;
}
</style>