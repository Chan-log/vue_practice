<template>
	<div class="black-bg" v-if="modal == true">
		<div class="white-bg">
			<img :src="rooms[clickId].image"  class="room-img">
			<h4>{{rooms[clickId].title}}</h4>
			<p>{{rooms[clickId].content}}</p>
			<input type="number" v-model.number="month">
			<p id = "price">{{month}}개월 : {{month * rooms[clickId].price}}원</p>
			<button class="modal-button" @click="$emit('closeModal'); month=1">닫기</button>
		</div>
	</div>
</template>

<script>
export default {
	name : 'ModalTable',
	data(){
		return {
			month : 1,
		}
	},
	watch : {
		month(a){
			if (typeof(a) == "string"){
				this.month = 0;
			}
		}
	},
	methods:{
	},
	props : {
		rooms : Object,
		clickId : Number,
		modal : Boolean,
	}
}
</script>

<style>

</style>