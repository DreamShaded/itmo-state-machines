<template>
  <div class="explosion-img-wrapper">
    <img :src="currentImage" alt="Визуализация" class="explosion-img" />
  </div>
</template>

<script setup>
import { computed } from "vue";
import { useSlideContext } from "@slidev/client";

const props = defineProps({
	images: { type: Array, required: true },
});

const { $clicks } = useSlideContext();
const currentImage = computed(() => {
	const currentClicks = $clicks?.value || 0;
	const index = Math.min(currentClicks, props.images.length - 1);
	return props.images[index] || props.images[0];
});
</script>

<style scoped>
.explosion-img-wrapper {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	width: 100%;
	height: 100%;
	display: grid;
	place-items: center;
}

.explosion-img {
	max-width: 100%;
	max-height: 60vh;
	object-fit: contain;
	display: block;
}
</style>

