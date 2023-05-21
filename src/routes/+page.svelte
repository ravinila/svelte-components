<script lang="ts">
	import Tabs from '$lib/components/Tabs/index.svelte';
</script>

<br />

<Tabs onTabChange={(a, b) => console.log('tab changed', a, b)} />
