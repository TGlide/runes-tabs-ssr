<script>
	import { getContext } from 'svelte';

	const { children } = $props();
	const { initContent } = getContext('tabs');
	initContent(() => children);
</script>
