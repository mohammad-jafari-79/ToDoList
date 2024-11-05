<template>
  <div class="grid-container">
    <header class="item-1">
      <p>My To Do List</p>
      <div>
        <input v-model.trim="newText" type="text" placeholder=" type somthing">
        <button @click="addItem" v-bind:disabled="newText.length == 0" class="btn active-button">Add</button>
      </div>
    </header>
    <section class="item-2" v-if="showList">
      <ul>
        <li 
        v-for="(item, index) in textList" 
        :key="index"
        @click="checkingItems(item)"
        :class="{checked: item.isChecked}">
          <h3>{{item.lable}}</h3> 
          <button @click="removeItem(index)" class="remove">x</button>
        </li>
      </ul>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const newText = ref('')
const showList = ref(false)
const textList = ref([])
const addItem = ()=>{
  showList.value = true
  textList.value.push({lable:newText.value, isChecked: false})
  newText.value = ""
}
const checkingItems = (item)=>{
  item.isChecked = !item.isChecked
}
const removeItem = (index)=>{
  textList.value.splice(index, 1)
}

</script>

<style scoped>

.grid-container{
  display: grid;
  width: 100%;
  height: 50%;
  margin-top: 10rem;
  grid-template-columns: 20% 20% 20% 20%;
  row-gap: 1rem;
  padding: 2rem 0;
}
.item-1{
  background-color: rgb(41, 128, 185);
  color: white;
  padding: 2rem 2rem;
  grid-column: 2/5;
  border-radius: 1rem;
}
.item-1 p{
  font-size: 1.4rem;
  text-align: center;
  margin-bottom: .5rem;
}
.item-1 div{
  display: flex;
  justify-content: center;
}
.item-2{
  padding: 1.5rem 0;
  grid-column: 2/5;
}
.active-button{
  background-color: rgb(155, 89, 182);
  color: white;
  padding: 0 .5rem;
  margin-left: .2rem;
}
.active-button:hover{
  background-color: rgb(142, 68, 173);
  color: white;
}
ul{
  padding: 1rem;
  display:table;
  width:100%;
  box-sizing:border-box;
  background-color: rgb(52, 152, 219);
  list-style-type: none;
  border-radius: 1rem;
}
ul li{
  width: 100%;
  position: relative;
  cursor: pointer;
  margin-bottom: 2rem;
  padding: .7rem .33rem .7rem 2.5rem;
  background-color: rgb(236, 236, 236);
  transition: 0.2s;
  border-radius: 1rem;
}
ul li:hover{
  background-color: rgb(182, 182, 182);
}
.checked {
  text-decoration: line-through;
  color: rgb(127, 140, 141);
}
ul li .remove{
  position: absolute;
  color: rgb(116, 116, 116);
  cursor: pointer;
  right: 0;
  top: 0;
  padding: .7rem 1rem;
  border: none;
  padding: 0 1.3rem;
  height: 100%;
  border-radius: 0 1rem 1rem 0;
}
ul li .remove:hover{
  color: white;
  background-color: red;
}
.btn[disabled] {
  background: #8795a1;
}

.btn[disabled]:hover {
  background: #606f7b;
}

</style>
