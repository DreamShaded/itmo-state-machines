<template>
	<div class="automata-diagram-wrapper">
		<div v-if="currentDiagram === 'moore'" class="automata-diagram">
			<img src="/images/automatas/moore.svg" alt="Автомат Мура" />
		</div>
		
		<div v-if="currentDiagram === 'mealy'" class="automata-diagram">
			<img src="/images/automatas/Mili.svg" alt="Автомат Милли" />
		</div>
	</div>
</template>

<script setup>
import { computed } from "vue";
import { useSlideContext } from "@slidev/client";

const { $clicks } = useSlideContext();
const currentDiagram = computed(() => {
	const currentClicks = $clicks?.value || 0;
	// Клик 1: показываем Мура (когда появляется первый пункт о Мура)
	// Клик 2+: показываем Милли (когда появляется второй пункт о Милли и дальше)
	if (currentClicks <= 1) return "moore";
	return "mealy"; // начиная со второго клика показываем Милли
});
</script>

<style scoped>
.automata-diagram-wrapper {
	position: relative;
	width: 100%;
	min-height: 400px;
	display: flex;
	align-items: center;
	justify-content: center;
}

.automata-diagram {
	width: 100%;
	display: flex;
	align-items: center;
	justify-content: center;
}

.automata-diagram img {
	width: 100%;
	max-width: 500px;
	height: auto;
	display: block;
	object-fit: contain;
}
</style>

