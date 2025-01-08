<script lang="ts">
	import Text from './Text.svelte';
	import { createEventDispatcher } from 'svelte';
	export let name: string;
	export let value: number;
	export let auto: number;

	const dispatch = createEventDispatcher();
	let textField: Text;

	export let detail: {
		options: string[];
		secondaryToggles?: string[];
		secondaryToggleValues?: boolean[];
		customOption?: boolean;
		customOptionValue?: string;
	};

	$: palette = auto == value ? 'accent-secondary' : 'accent';
	$: {
		if (detail.secondaryToggleValues) { // If secondaryToggleValues updates we need to force an update up the chain
			dispatch('forceUpdate');
		} else if (detail.secondaryToggles) { // Set all toggles to false if undefined
			detail.secondaryToggles.forEach((toggle, index) => {
				if (!detail.secondaryToggleValues) detail.secondaryToggleValues = [];
				detail.secondaryToggleValues[index] = false; 
			});
		}
	}
</script>

<div class={`top palette-${palette}`}>
	<div class="background">
		<div
			class="switch"
			style={`--pos:calc(${value} * (var(--button-size) + var(--padding) * 2) + var(--padding) / 2`}
		/>
	</div>
	<ul>
		{#each detail.options as option, index}
			<label class="radioLabel">
				<input class="radioInput" type="radio" bind:group={value} {name} checked={index == value} value={index} />
				<li>
					<p>
						{option}
					</p>
					{#if index == auto}
						<p class="optionInfo">default</p>
					{/if}
					{#if detail.secondaryToggles && detail.secondaryToggles[index] && detail.secondaryToggleValues}
						<label class={`palette-${palette} toggleLabel`}>
							<div>
								<input class="toggleInput" type="checkbox" bind:checked={detail.secondaryToggleValues[index]}/>
								<p> {detail.secondaryToggles[index]} </p>
								<div class="toggleBackground">
									<div class="toggleSwitch"/>
								</div>
							</div>
						</label>
					{/if}
				</li>
			</label>
		{/each}
		{#if detail.customOption && detail.customOptionValue != null}
			<label class="radioLabel">
				<input
					type="radio"
					class="radioInput"
					bind:group={value}
					{name}
					checked={value == detail.options.length}
					value={detail.options.length}
				/>
				<li>
					<Text
						placeholder="custom"
						nowrap={true}
						bind:value={detail.customOptionValue}
						bind:this={textField}
						on:input={() => (dispatch('forceUpdate'))}
						on:focus={() => (value = detail.options.length)}
					/>
					{#if detail.customOptionValue != ''}
						<p class="optionInfo">custom</p>
					{/if}
				</li>
			</label>
		{/if}
	</ul>
</div>

<style>
	.top {
		display: flex;
		flex-direction: row;
		position: relative;
		width: auto;
	}
	.background {
		position: relative;
		box-sizing: content-box;
		padding: var(--padding-small);
		width: var(--button-size);
		height: auto;
		background-color: var(--this-background-indent);
		border-radius: var(--border-radius);
		transition: background var(--transition-speed);
		margin: calc(var(--padding-small)) 0;
	}
	.top:hover > .background {
		background-color: var(--this-background-active);
	}
	.switch {
		position: absolute;

		box-sizing: content-box;
		padding: calc(var(--padding-small) - var(--padding-small));
		width: var(--button-size);
		height: var(--button-size);
		left: var(--padding-small);
		top: var(--pos);

		border: none;
		background-color: var(--this-color);
		color: var(--this-text);
		border-radius: var(--border-radius);
		transition: background var(--transition-speed), top var(--transition-speed),
			color var(--transition-speed);
	}

	ul {
		list-style: none;
		box-sizing: border-box;
		padding: 0;
		margin: 0;
		width: calc(100% - var(--button-size) - var(--padding));
		display: block;
	}
	.radioLabel {
		position: relative;
		height: calc(var(--button-size) + var(--padding) * 2);
		margin-left: calc(-1 * (var(--button-size) + var(--padding)));
		display: block;
		padding-right: var(--padding);
		padding-left: calc(var(--button-size) + var(--padding) * 2);
		font-size: inherit;
		z-index: 2;
	}
	p {
		margin: 0;
		height: min-content;
	}

	.radioLabel > li {
		display: flex;
		flex-direction: row;
		height: calc(var(--button-size) + var(--padding-small) * 2);
		padding: calc(var(--padding) / 2) var(--padding) calc(var(--padding) / 2) var(--padding);
		border-radius: var(--border-radius);
		align-items: center;
	}
	.radioLabel:hover > li {
		background-color: var(--this-background-indent);
	}
	.radioLabel:active > li {
		background-color: var(--this-background-active);
		color: var(--this-text);
	}
	input {
		display: none;
	}
	input:checked + li {
		color: var(--this-text);
	}
	.optionInfo {
		opacity: 0;
		margin-left: var(--padding);
		color: var(--this-text-weak);
		transition: opacity var(--transition-speed);
		width: min-content;
	}
	.radioLabel:hover > li > .optionInfo {
		opacity: 1;
	}
	.toggleLabel {
		margin-left: auto;
		padding: 0;
		height: min-content;
		pointer-events: none;
	}
	.radioInput:checked + li > .toggleLabel {
		pointer-events: all;
	}
	.toggleLabel > div {
		display: grid;
		grid-template-columns: auto auto; 
  		grid-template-rows: 1fr;
		width: auto;
		align-items: center;
		opacity: 0;
		transition: opacity var(--transition-speed);
	}
	.toggleLabel > div > p {
		padding-right: var(--padding);
	}
	.radioInput:checked + li > .toggleLabel > div {
		opacity: 1;
	}
	.toggleBackground {
		position: relative;
		box-sizing: content-box;
		padding: var(--padding-small);
		width: calc(var(--button-size) * 2);
		height: var(--button-size);
		background-color: var(--this-background-indent);
		border-radius: var(--border-radius);
		transition: background var(--transition-speed), filter var(--transition-speed);
	}
	.radioLabel:hover > li > .toggleLabel > div >.toggleBackground {
		filter: saturate(0.2);
	}
	.toggleBackground:hover {
		background-color: var(--this-background-active);
	}
	.toggleSwitch {
		position: absolute;
		display: flex;
		flex-direction: row;
		align-items: center;

		box-sizing: content-box;
		padding: calc(var(--padding-small) - var(--padding-small));
		width: var(--button-size);
		height: var(--button-size);
		left: var(--padding-small);
		top: var(--padding-small);

		border: none;
		background-color: var(--this-color);
		color: var(--this-text);
		border-radius: var(--border-radius);
		transition: background var(--transition-speed), left var(--transition-speed),
        color var(--transition-speed);
	}
	.toggleInput:checked ~ .toggleBackground > .toggleSwitch {
    	left: calc(var(--button-size) + var(--padding-small));
  	}
</style>
