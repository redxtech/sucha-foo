<script setup lang="ts">
defineProps({
	isWebcamShowing: Boolean,
})
</script>

<template>
	<h1 v-if="isWebcamShowing">you're sucha foo !</h1>
	<h1 v-else>who's sucha foo ?</h1>
</template>

<style scoped>
h1 {
	font-size: 3.2em;
	line-height: 1.1;
}
</style>
