<script lang="ts">
	import { cn } from '$lib/utils';
	import { Button } from '../button';
	import { getEmblaContext } from './context';
	import type { HTMLAttributes } from 'svelte/elements';

	type DotsProps = {
		use_countdown_dots?: { active: boolean; delay: number };
	} & HTMLAttributes<HTMLDivElement>;

	type $$Props = DotsProps;

	let className: $$Props['class'] = undefined;
	export { className as class };
	export let use_countdown_dots = { active: false, delay: 4000 };

	const { handleKeyDown, scrollTo, scroll_snaps, selected_index } =
		getEmblaContext('<Carousel.Dots/>');
</script>

<!-- TODO: On small screen, make it one long progress/scroll bar -->
<div class="mx-auto mt-4 flex w-fit max-w-full items-center gap-2 overflow-x-auto">
	{#each $scroll_snaps as _, i}
		{@const is_active = $selected_index === i}
		<Button
			size="sm"
			variant="outline"
			on:click={() => scrollTo(i)}
			on:keydown={handleKeyDown}
			class={cn('relative h-2 w-[35px] rounded-full bg-muted', className)}
		>
			{#if is_active && use_countdown_dots.active === true}
				{@const in_seconds = use_countdown_dots.delay / 1000}
				<div
					style="--countdown-delay: {in_seconds}s"
					class={cn('absolute inset-0 rounded-full', { countdown: is_active })}
				/>
			{/if}
		</Button>
	{/each}
</div>

<style>
	.countdown {
		animation: fill var(--countdown-delay) linear 1;
		background-color: hsl(var(--primary));
	}

	@keyframes fill {
		0% {
			width: 0%;
		}
		100% {
			width: 100%;
		}
	}
</style>
