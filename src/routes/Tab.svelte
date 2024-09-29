<script>
	import { getContext } from 'svelte';

	const { children } = $props();
	const { initTab } = getContext('tabs');
	initTab(() => children);
</script>
