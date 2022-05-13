<style>
	.loader {
		position: relative;
		height: 100%;
		width: 100%;
		padding: 40px;
		z-index: 2;
	}
	.loader:before {
		content: '';
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		height: 50px;
		width: 50px;
		border: 2px solid #111;
		border-left: 2px solid transparent;
		border-radius: 50%;
		animation: loading 500ms linear infinite;
	}
	@keyframes laoding {
		100% {
			transform: translate(-50%, -50%) rotate(360deg);
		}
	}
</style>

<div class="loader" />
