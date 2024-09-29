<script>
	import Tabs from './Tabs.svelte';
	import Tab from './Tab.svelte';
	import TabContent from './TabContent.svelte';
</script>

<Tabs>
	<Tab>Tab 1</Tab>
	<TabContent>Inside Tab 1</TabContent>

	<Tab>Tab 2</Tab>
	<TabContent>Inside Tab 2</TabContent>

	<Tab>Tab 3</Tab>
	<TabContent>Inside Tab 3</TabContent>
</Tabs>

<style>
	/* Theme */
	:root {
		--tab-bg: #eee;
		--content-bg: #fff;
		--content-border: #000;
	}
	:global(.dark) {
		--tab-bg: #000;
		--content-bg: #000;
		--content-border: #fff;
	}
	:global(*) {
		box-sizing: border-box;
	}
</style>
