<template>
	<div>
		<input v-model="text" />
		<button @click="post()">Post</button>
		<div v-for="message in messages" v-bind:key="message">
			{{ message }}
		</div>
	</div>
</template>
<script setup>
import Gun from "gun";
import { ref } from "vue";

let gun = Gun(["localhost:3000"]);

let copy = gun.get("test").get("paste");

let messages = [];

const text = ref("");

function post() {
	console.log(text.value);
	copy.put(text.value);
}

copy.on((data) => {
	messages.push(data);
});
</script>
