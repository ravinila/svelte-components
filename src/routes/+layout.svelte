<script lang="ts">
	import { dev } from '$app/environment';
</script>

<slot />
{#if dev}
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap"
		rel="stylesheet"
	/>
{/if}

<style>
	:global(:root) {
		--fz-normal: 12px;
	}
	:global(body) {
		margin: 0;
		padding: 0;
		font-family: 'Roboto', sans-serif;
		font-size: 16px;
		line-height: 1.5;
		background-color: #333;
	}
</style>
