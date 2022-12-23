<script lang="ts">
	let videoElement: HTMLVideoElement | null;

	let hideCursor = false;

	const leaveFullscreen = () => {
		hideCursor = false;
		document.removeEventListener('keydown', controlVideoPlaybackPlay);
		document.removeEventListener('keyup', controlVideoPlaybackReset);
		document.removeEventListener('fullscreenchange', leaveFullscreen);
	};

	const switchToFullscreen = () => {
		if (!videoElement || !videoElement.requestFullscreen) {
			return;
		}
		videoElement.requestFullscreen();
		document.addEventListener('keydown', controlVideoPlaybackPlay);
		document.addEventListener('keyup', controlVideoPlaybackReset);
		hideCursor = true;
		setTimeout(() => {
			document.addEventListener('fullscreenchange', leaveFullscreen);
		}, 100);
	};

	const controlVideoPlaybackPlay = (event: KeyboardEvent) => {
		if (event.isComposing || event.repeat || !videoElement || event.key !== ' ') {
			return;
		}
		videoElement.play();
	};

	const controlVideoPlaybackReset = (event: KeyboardEvent) => {
		if (event.isComposing || event.repeat || !videoElement || event.key !== ' ') {
			return;
		}
		videoElement.pause();
		videoElement.currentTime = 0;
	};
</script>

<div class="container">
	<video
		class="video"
		bind:this={videoElement}
		on:click={(e) => {
			e.preventDefault();
		}}
		class:hideCursor
	>
		<source src="my_video.mp4" type="video/mp4" />
	</video>
	<p>Click the "start experiment button and then press the spacebar.</p>
	<button class="button" on:click={switchToFullscreen}>Start the experiment</button>
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 100%;
	}

	video::-webkit-media-controls-enclosure {
		display: none !important;
	}
	.video {
		height: 50vh;
	}
	.hideCursor {
		cursor: none;
	}

	.button {
		margin-top: 3rem;
		padding: 1rem 1.5rem;
		border: none;
		border-radius: 0.25rem;
		background-color: #333;
		color: white;
		font-size: large;
	}
	.button:hover {
		background-color: #555;
	}
</style>
