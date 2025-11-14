<template>
	<div class="traffic-light-demo">
		<div class="traffic-light">
			<div
				class="light light-red"
				:class="{ active: state === 'red' }"
			></div>
			<div
				class="light light-yellow"
				:class="{ active: state === 'yellow' }"
			></div>
			<div
				class="light light-green"
				:class="{ active: state === 'green' }"
			></div>
		</div>
		<button @click="next" class="traffic-btn">Следующее состояние</button>
	</div>
</template>

<script setup>
import { ref } from "vue";

const state = ref("red");
const prevState = ref(null);

function next() {
	if (state.value === "red") {
		prevState.value = "red";
		state.value = "yellow";
	} else if (state.value === "yellow") {
		if (prevState.value === "red") {
			prevState.value = "yellow";
			state.value = "green";
		} else {
			prevState.value = "yellow";
			state.value = "red";
		}
	} else if (state.value === "green") {
		prevState.value = "green";
		state.value = "yellow";
	} else {
		state.value = "red";
	}
}
</script>

<style scoped>
.traffic-light-demo {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	gap: 2rem;
	height: 100%;
}

.traffic-light {
	display: flex;
	flex-direction: column;
	gap: 1rem;
	padding: 2rem;
	background: #1f2937;
	border-radius: 1rem;
}

.light {
	width: 80px;
	height: 80px;
	border-radius: 50%;
	background: #374151;
	transition: opacity 0.3s;
	opacity: 0.3;
}

.light.active {
	opacity: 1;
}

.light-red.active {
	background: #dc2626;
	box-shadow: 0 0 20px #dc2626;
}

.light-yellow.active {
	background: #fbbf24;
	box-shadow: 0 0 20px #fbbf24;
}

.light-green.active {
	background: #16a34a;
	box-shadow: 0 0 20px #16a34a;
}

.traffic-btn {
	padding: 0.75rem 1.5rem;
	background: #3b82f6;
	color: white;
	border: none;
	border-radius: 0.5rem;
	font-size: 1rem;
	cursor: pointer;
	transition: background 0.2s;
}

.traffic-btn:hover {
	background: #2563eb;
}
</style>

