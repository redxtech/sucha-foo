<script setup lang="ts">
import { ref, onMounted } from 'vue'

const player = ref<HTMLVideoElement | null>(null)

// when the component is mounted, start the webcam
onMounted(() => {
	if (navigator.mediaDevices.getUserMedia) {
		navigator.mediaDevices
			.getUserMedia({ video: true })
			.then(function (stream) {
				// video.srcObject = stream;
				if (player.value) player.value.srcObject = stream
			})
			.catch(function (err0r) {
				console.log('Something went wrong!')
				console.error(err0r)
			})
	}
})
</script>

<template>
	<div class="webcam">
		<video id="player" ref="player" autoplay></video>
	</div>
</template>

<style scoped>
.webcam {
	width: 100%;
	height: auto;
	display: flex;
	justify-content: center;
}

#player {
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
</style>
