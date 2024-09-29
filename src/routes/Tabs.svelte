<script lang="ts">
	import { setContext, type Snippet } from 'svelte';
	const { children }: { children: Snippet } = $props();

	let tabs = $state<Snippet[]>([]);
	let contents = $state<Snippet[]>([]);
	let selected = $state(0);

	setContext('tabs', {
		initTab(getChildren: () => Snippet) {
			const index = tabs.length;

			tabs[index] = getChildren();
			$effect.pre(() => {
				tabs[index] = getChildren();
			});

			// TODO: deal with unmount
		},
		initContent(getChildren: () => Snippet) {
			const index = contents.length;

			contents[index] = getChildren();
			$effect.pre(() => {
				contents[index] = getChildren();
			});

			// TODO: deal with unmount
		}
	});

	const randomName = Math.random().toString(36).substring(2, 7);

	function buildCSS() {
		return (
			'<style>' +
			tabs
				.map((_, i) => {
					return `
			  :has([data-tab='${i}'] :checked) [data-tab-content='${i}']	{
				  display: block;
			  }`;
				})
				.join('') +
			'</style>'
		);
	}
</script>

{@render children()}

<div role="tablist">
	{#each tabs as tab, i}
		<label class="tab" data-tab={i}>
			<input
				id="tabs-{i}"
				name={randomName}
				role="tab"
				type="radio"
				checked={selected === i}
				onkeydown={() => (selected = i)}
				onclick={() => (selected = i)}
			/>
			{@render tab()}
		</label>
	{/each}
</div>

{#each contents as content, i}
	<div class="tab-contents" role="tabpanel" tabindex="0" data-tab-content={i}>
		{#if content}
			{@render content()}
		{/if}
	</div>
{/each}

{@html buildCSS()}

<style>
	.tab {
		display: inline-block;
		background-color: var(--tab-bg, #eee);
		padding: 0.5rem;
		margin: 0;
		cursor: pointer;
	}
	.tab:focus-within {
		outline: 2px solid var(--content-border);
	}
	.tab:has(:checked) {
		border: 1px solid var(--content-border);
	}
	input[role='tab'] {
		appearance: none;
		position: absolute;
		padding: 0;
	}

	.tab-contents {
		background-color: var(--content-bg, #fff);
		border: 1px solid var(--content-border, #000);
		padding: 1rem;
		display: none;
	}
</style>
