<script setup lang="ts">
import { ref, onMounted } from 'vue'
import PageTitle from './PageTitle.vue'

const webcam = ref<HTMLVideoElement | null>(null)
const isWebcamShowing = ref(false)

// when the component is mounted, start the webcam
onMounted(async () => {
	try {
		if (navigator.mediaDevices.getUserMedia) {
			const stream = await navigator.mediaDevices.getUserMedia({
				video: { facingMode: 'user' },
			})

			if (webcam.value) webcam.value.srcObject = stream
			isWebcamShowing.value = true
			console.log("you've been foo'd !")
		}
	} catch (err) {
		console.error('something went wrong:', err)
	}
})
</script>

<template>
	<PageTitle v-if="isWebcamShowing" />
	<div class="webcam">
		<video ref="webcam" autoplay></video>
	</div>
</template>

<style scoped>
.webcam {
	width: 100%;
	height: auto;
	display: flex;
	justify-content: center;

	:is(video) {
		width: 100%;
		height: auto;

		/* mirror webcam video to look more natural */
		-moz-transform: scale(-1, 1);
		-webkit-transform: scale(-1, 1);
		-o-transform: scale(-1, 1);
		transform: scale(-1, 1);
		filter: FlipH;
		-ms-filter: 'FlipH';
	}
}
</style>
