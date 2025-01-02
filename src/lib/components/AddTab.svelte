<script lang="ts">
	import Button from './Button.svelte';
	import TutorialHighlight from './TutorialHighlight.svelte';
	import { debateStyleMap, currentDebateStyleFlow, debateStyles, type DebateStyleFlow } from '$lib/models/debateStyle';
	import { settings } from '$lib/models/settings';
	import { onDestroy } from 'svelte';

	export let addFlow: (type: DebateStyleFlow) => void;
	export let switchSpeakers: boolean;

	let debateStyleIndex = settings.data['debateStyle'].value as number;
	onDestroy(
		settings.subscribe(['debateStyle'], (key: string) => {
			debateStyleIndex = settings.data[key].value as number;
		})
	);
	onDestroy(
		() => {
			console.log("Gone!")
		}
	);
	$: debateStyle = debateStyles[debateStyleMap[debateStyleIndex]];

	let primaryFlow: DebateStyleFlow | null;
	let secondaryFlow: DebateStyleFlow | null;

	let hasSwitch: boolean;
	$: { // Update when debateStyleIndex changes
		if (debateStyleIndex !== undefined) {  };
		primaryFlow = currentDebateStyleFlow("primary");
		secondaryFlow = currentDebateStyleFlow("secondary");
		if (primaryFlow != null) {
			hasSwitch = primaryFlow.columnsSwitch != null;
		}
	}
	
	function flipPairs(arr: DebateStyleFlow[]) {
		// produce new array where [0,1,2,3] => [1,0,3,2]
		const result = [];
		for (let i = 0; i < arr.length; i += 2) {
			if (arr[i + 1]) {
				result.push(arr[i + 1]);
				result.push(arr[i]);
			} else {
				result.push(arr[i]);
			}
			}
		return result;
	}

  	$: flippedStyleTemplates = flipPairs(debateStyle.templates);

	$: currentStyleTemplates = switchSpeakers
    ? flippedStyleTemplates
    : debateStyle.templates;

</script>

<div class="addTab" class:hasSwitch class:switch={switchSpeakers}>
	<div class="buttons">
		{#each currentStyleTemplates as flow, index}
			{#if index === 0 || index === 1}
				<TutorialHighlight step={5 + index}> <!-- 5 is a magic number. It is the starting step when the add tab is shown  -->
					<!-- index % 2 === (switchSpeakers ? 1 : 0) can be used instead of !flow.invert for mandatory flip-flop colors -->
					<Button
						text={flow.name}
						palette={!flow.invert ? "accent" : "accent-secondary"}  
						icon="add"
						on:click={() => addFlow(flow)}
						tooltip={`create new ${flow.name} flow`}
						shortcut={
							index === 0 
								? ['control', 'n'] 
								: index === 1 
									? ['control', 'shift', 'n'] 
									: null
						}
					/>
				</TutorialHighlight>
			{/if}
			{#if index > 1} <!-- Only use the first two buttons in the tutorial -->
				<Button
					text={flow.name}
					palette={!flow.invert ? "accent" : "accent-secondary"}
					icon="add"
					on:click={() => addFlow(flow)}
					tooltip={`create new ${flow.name} flow`}
					shortcut={
						index === 0 
							? ['control', 'n'] 
							: index === 1 
								? ['control', 'shift', 'n'] 
								: null
					}
				/>
			{/if}
		{/each}
	</div>
	{#if primaryFlow != null && secondaryFlow != null && hasSwitch}
		<div class="switch">
			<Button
				text={'first'}
				icon="arrowLeft"
				palette={switchSpeakers ? 'accent-secondary' : 'accent'}
				tooltip={switchSpeakers
					? `set ${primaryFlow.name} to first speaker`
					: `set ${secondaryFlow.name} to first speaker`}
				on:click={() => (switchSpeakers = !switchSpeakers)}
			/>
		</div>
	{/if}
</div>

<style>
	.buttons {
		display: flex;
		position: relative;
		flex-wrap: wrap;
		align-items: stretch;
		flex-direction: row;
		gap: var(--padding);
	}
	.hasSwitch .buttons {
		flex-direction: column;
	}
	.addTab.hasSwitch {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
	}
</style>
