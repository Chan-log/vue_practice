<template>
    <!-- <div v-for="(product,i) in rooms" :key="i" @click="modal = true; clickId = i"> -->
	<div @click="$emit('openModal', rooms.id)">
		<img :src="rooms.image"  class="room-img">
		<h4>{{rooms.title}}</h4>
		<p>{{rooms.content}}</p>
		<p>{{rooms.price}}원</p>
    </div>
</template>

<script>
export default {
	name: 'MainTable',
	props : {
		rooms : Object,
	}
}
</script>

<style>

</style>