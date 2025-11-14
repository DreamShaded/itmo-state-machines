<template>
	<div class="code-phone-wrapper">
		<div class="phone-frame">
			<div class="phone-screen">
				<pre class="code-content"><code>{{ code }}</code></pre>
			</div>
		</div>
	</div>
</template>

<script setup>
defineProps({
	code: {
		type: String,
		required: true,
	},
});
</script>

<style scoped>
.code-phone-wrapper {
	width: 100%;
	height: 100%;
	display: grid;
	place-items: center;
}

.phone-frame {
	position: relative;
	width: 100%;
	max-width: 400px;
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
	overflow: auto;
	background: var(--background);
	padding: 1rem;
}

.code-content {
	margin: 0;
	padding: 0;
	color: var(--color);
	font-family: "Fira Code", "Courier New", monospace;
	font-size: 0.7rem;
	line-height: 1.6;
	white-space: pre-wrap;
	word-wrap: break-word;
}

.code-content code {
	color: inherit;
	font-family: inherit;
}
</style>

