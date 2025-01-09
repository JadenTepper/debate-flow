<script lang="ts">
	import Toggle from './Toggle.svelte';
	import Radio from './Radio.svelte';
	import Slider from './Slider.svelte';
	import Button from './Button.svelte';
	import { settings, type Setting } from '$lib/models/settings';
	import { tweened } from 'svelte/motion';
	import { onDestroy } from 'svelte';
	export let setting: Setting;
	export let key: string;

	let value: any = setting.value;
	let secondaryToggleValues: boolean[] | undefined;

	function setValue(value: any) {
		settings.setValue(key, value);
	}
	$: value, setValue(value);
	$: {
		if (setting.type == "radio") {
			secondaryToggleValues, setValue(value);
		}
	}

	function resetValue() {
		if (setting.type == 'radio' && setting.detail.secondaryToggleValues && setting.detail.secondaryToggleAutos) {
			setting.detail.secondaryToggleValues = [...setting.detail.secondaryToggleAutos]; // Resets toggles
		}

		settings.setValue(key, setting.auto);
		value = setting.value;
	}

	
	function arraysAreEqual<T>(arr1: T[], arr2: T[]): boolean{
    	return arr1.length === arr2.length && arr1.every((val, index) => val === arr2[index]);
	}

	let showResetButton = false;
	onDestroy(
		settings.subscribe([key], function (key) {
			if (setting.value != value) {
				value = setting.value;
			}

			if (setting.type == 'radio' && setting.detail.secondaryToggleValues != secondaryToggleValues) {
				secondaryToggleValues = setting.detail.secondaryToggleValues;
			}

			showResetButton = (
				value !== setting.auto ||
				setting.type === 'radio' &&
				setting.detail.secondaryToggleValues &&
				setting.detail.secondaryToggleAutos &&
				!(arraysAreEqual(setting.detail.secondaryToggleValues, setting.detail.secondaryToggleAutos))
			) as boolean;
		})
	);

	let spotlight = tweened(0);
	let element: HTMLElement;
	export function scrollToSelf() {
		element.scrollIntoView();
		spotlight = tweened(1, {
			duration: 2000
		});
		$spotlight = 0;
	}
</script>

<div class="top" bind:this={element} style={`--spotlight:${$spotlight}`}>
	<span class="above">
		<div class="titleReset">
			<h2>{setting.name}</h2>
			<div class="reset" class:hidden={!showResetButton}>
				<Button
					icon="arrowRoundLeft"
					tooltip="reset to default"
					tooltipLayout="right"
					on:click={resetValue}
				/>
			</div>
		</div>

		{#if setting.type == 'toggle'}
			<Toggle bind:value auto={setting.auto} />
		{/if}
		{#if setting.info && setting.type != 'toggle'}
			<p class="info">{setting.info}</p>
		{/if}
	</span>
	{#if setting.type == 'radio'}
		<Radio
			name={setting.name}
			bind:value
			bind:secondaryToggleValues
			auto={setting.auto}
			bind:detail={setting.detail}
			on:forceUpdate={() => setValue(value)}
		/>
	{/if}
	{#if setting.type == 'slider'}
		<Slider bind:value auto={setting.auto} bind:detail={setting.detail} />
	{/if}
	{#if setting.info && setting.type == 'toggle'}
		<p class="info">{setting.info}</p>
	{/if}
</div>

<style>
	.top {
		position: relative;
		border-radius: var(--border-radius);
		padding: var(--padding);
		max-width: 30rem;
		min-width: 10rem;
		width: 100%;
		box-sizing: border-box;
	}

	.above {
		position: relative;
		display: flex;
		flex-direction: row;
		gap: 1em;
		height: var(--button-size);
		align-items: center;
		padding-bottom: var(--padding);
		height: 100%;
	}
	.above h2 {
		width: max-content;
		white-space: nowrap;
	}
	.above .titleReset {
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: 1em;
	}
	p.info {
		color: var(--this-text-weak);
		opacity: 0;
		transition: opacity var(--transition-speed);
		margin: 0;
	}
	.top:hover p.info {
		opacity: 1;
	}
	.hidden {
		color: var(--this-text-weak);
	}
	.reset {
		opacity: 1;

		transition: opacity var(--transition-speed);
	}
	.reset.hidden {
		opacity: 0;
	}
	@media (max-width: 800px) {
		.above {
			flex-direction: column;
			align-items: flex-start;
			gap: 0;
		}
	}
</style>
