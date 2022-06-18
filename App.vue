<template>
  <transition name="fade">
    <Modal @closeModal="modal=false" :rooms = "rooms" :modal = "modal" :clickId="clickId" />
  </transition>
    <div class="menu">
      <a v-for="(nav, i) in menu" :key="i">{{nav}}</a>
    </div>
<Discount/>

<button @click="priceSort">가격 순 정렬</button>
<Table @openModal="modal=true; clickId = $event" :rooms = "rooms[i]" v-for="(a, i) in rooms" :key="a"/>

</template>

<script>

import roomData from './assets/rooms';
import Discount from './components/Discount.vue';
import Table from './components/Table.vue';
import Modal from './components/Modal.vue';

export default {
  name: 'App',
  data(){
    return{
      modal: false,
      police: [0, 0, 0],
      products : [{name : '역삼동', imgUrl : require("./assets/room0.jpg")}, {name : '천호동', imgUrl : require("./assets/room1.jpg")}, {name : '마포구' , imgUrl : require("./assets/room2.jpg")}],
      menu : ['Home', 'Products', 'About'],
      price : [60, 70, 80],
      rooms : roomData,
      clickId : 0,
    }
  },
  methods:{
    priceSort(){
      
    }
  },
  components: {
    Discount : Discount,
    Table: Table,
    Modal: Modal,
  }
}
</script>

<style>

  * {

    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }

body{
  margin : 0;
}
div {
  box-sizing: border-box;
}

.black-bg {
  width: 100%;
  height: 100%;
  background:rgba(36,36,36,0.7);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
.modal-button {
  background-color: #3a3b3a;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu{
  background: #363636;
  padding: 15px;
  border-radius: 5px;
}
.menu a{
  color:white;
  padding: 10px;
}
.room-img{
  width: 100%;
  margin-top: 40px;
  max-width: 900px;
}

.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  opacity: 1;
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

</style>
