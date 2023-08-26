<script setup lang="ts">
import { ref, onMounted } from 'vue'
import PageTitle from './PageTitle.vue'

const player = ref<HTMLVideoElement | null>(null)
const playerShown = ref(false)

// when the component is mounted, start the webcam
onMounted(async () => {
	try {
		if (navigator.mediaDevices.getUserMedia) {
			const stream = await navigator.mediaDevices.getUserMedia({
				video: { facingMode: 'user' },
			})

			if (player.value) player.value.srcObject = stream
			playerShown.value = true
			console.log("foo'd")
		}
	} catch (err) {
		console.error('Something went wrong:', err)
	}
})
</script>

<template>
	<PageTitle v-if="playerShown" />
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
