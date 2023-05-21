<script lang="ts">
	export const data: any = null;
	export const isActive: boolean = false;
	const className = '';
	export { className as class };
</script>

<button class="holder {className}" class:active={isActive} on:click>
	<slot />
</button>

<style lang="scss">
	.holder {
		display: flex;
		all: unset;
	}
</style>
