<script lang="ts">
	import { onMount } from 'svelte';
	import { writable } from 'svelte/store';
	import Tab from './Tab.svelte';

	export interface Tab {
		id: string;
		name: string;
		active: boolean;
	}

	export const tabs: Tab[] | string[] = [
		{ id: 'topics', name: 'Topics', active: true },
		{ id: 'science', name: 'Science', active: false },
		{ id: 'nature', name: 'Nature', active: false },
		{ id: 'politics', name: 'Politics', active: false },
		{ id: 'news', name: 'News', active: false }
	];

	// export const tabs: Tab[] | string[] = ['Topics', 'Science', 'Nature', 'Politics', 'News'];
	const className = '';
	export { className as class };
	export let activeTab = 0;
	export let onTabChange: (index: number, data?: Tab | string) => void = () => {};

	onMount(() => {
		const activeTab = tabs.findIndex((tab) => tab?.active);
		if (activeTab !== -1) setActiveTab(activeTab);
	});

	let container: HTMLDivElement;
	let activeTabElements: HTMLButtonElement[] = [];

	const setActiveTab = (index) => {
		activeTab = index;
		onTabChange(index, tabs[index]);
		moveFocus(index, activeTabElements[index]);
	};

	const moveFocus = (index, elem: HTMLButtonElement) => {
		container.style.setProperty('--active-tab-width', `${elem.offsetWidth}px`);
		container.style.setProperty('--active-tab-offset-left', `${elem.offsetLeft}px`);
	};
</script>

<div bind:this={container} class="tabs {className}">
	{#each tabs as tab, index}
		<button
			bind:this={activeTabElements[index]}
			class="tab"
			class:active={activeTab === index}
			on:click={() => setActiveTab(index)}
		>
			{tab.name}
		</button>
	{/each}
</div>

<style lang="scss">
	.tabs {
		--anim-delay: 0.4s;
		position: relative;
		display: flex;
		overflow-x: auto;
		max-width: 360px;
		margin: auto;
		gap: 10px;
		border-bottom: 1px solid #be093f;
		color: white;
		&::after {
			content: '';
			position: absolute;
			bottom: 0;
			left: 0;
			top: 0;
			width: 100px;
			background: #be093f;
			width: var(--active-tab-width);
			transform: translateX(var(--active-tab-offset-left));
			transition: transform var(--anim-delay) cubic-bezier(0.25, 0.4, 0.55, 1.2);
			z-index: -1;
			border-radius: 8px 8px 0px 0px;
		}

		&::-webkit-scrollbar {
			display: none;
		}

		:global(.tab) {
			border: 1px solid orange;
			all: unset;
			cursor: pointer;

			font-weight: 300;
			font-size: 12px;
			line-height: 14px;
			padding: 5px 10px;

			background-color: transparent;
			border-radius: 8px 8px 0px 0px;
			transition: background-color 0s linear;

			&.active {
				background-color: #be093f;
				transition-delay: var(--anim-delay);
				font-weight: 500;
				font-size: 12px;
				line-height: 14px;
			}
		}
	}
</style>
