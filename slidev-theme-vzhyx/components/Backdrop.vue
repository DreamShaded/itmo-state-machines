<template>
  <div class="backdrop-demo" ref="demoRef">
    <div class="phone-frame">
      <div class="phone-screen">
        <button class="backdrop-btn" @click="show = true">показать</button>
        <transition name="backdrop-slide">
          <div
            v-if="show"
            class="backdrop-overlay"
            @click="show = false"
          ></div>
        </transition>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const show = ref(false);
const demoRef = ref(null);

function handleClickOutside(event) {
	if (!demoRef.value) return;

	// если клик вне правого блока и backdrop показан - закрываем
	if (!demoRef.value.contains(event.target) && show.value) {
		show.value = false;
	}
}

onMounted(() => {
	document.addEventListener("click", handleClickOutside);
});

onBeforeUnmount(() => {
	document.removeEventListener("click", handleClickOutside);
});
</script>

<style scoped>
.backdrop-demo {
	position: relative;
	width: 100%;
	height: 100%;
	min-height: 300px;
	display: grid;
	place-items: center;
}

.phone-frame {
	position: relative;
	width: 280px;
	height: 500px;
	border: 8px solid var(--color);
	border-radius: 24px;
	padding: 8px;
	background: var(--background);
	box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}

.phone-screen {
	position: relative;
	width: 100%;
	height: 100%;
	border-radius: 16px;
	overflow: hidden;
	background: var(--background);
	display: grid;
	place-items: center;
}

.backdrop-btn {
	padding: 0.75rem 1.5rem;
	font-size: 1rem;
	background: var(--color);
	color: var(--background);
	border: none;
	border-radius: 0.5rem;
	cursor: pointer;
	font-weight: 600;
	transition: opacity 0.2s;
	z-index: 1;
}

.backdrop-btn:hover {
	opacity: 0.9;
}

.backdrop-overlay {
	position: absolute;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	background: lightblue;
	opacity: 0.85;
	cursor: pointer;
	z-index: 2;
}

/* анимация выезда справа налево */
.backdrop-slide-enter-active {
	transition: transform 0.3s ease-out;
}

.backdrop-slide-leave-active {
	transition: transform 0.3s ease-in;
}

.backdrop-slide-enter-from {
	transform: translateX(100%);
}

.backdrop-slide-leave-to {
	transform: translateX(100%);
}
</style>

