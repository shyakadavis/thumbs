<script lang="ts">
	import * as Carousel from '$lib/components/ui/carousel';

	const images = Array.from({ length: 10 }, (_, i) => `https://picsum.photos/seed/${i}/800/600`);
</script>

<section id="images" class="mx-auto max-w-7xl space-y-4 py-16">
	<div class="mx-auto max-w-xs rounded-xl bg-background/20 sm:max-w-full sm:px-16 sm:py-8">
		<Carousel.Root opts={{ loop: true, align: 'start' }}>
			<Carousel.Content>
				{#each images as image, i}
					<Carousel.Item class="sm:basis-1/3 lg:basis-1/5">
						<img
							src={image}
							alt="Something"
							class="rounded object-cover md:h-[233px] md:w-[240px]"
						/>
					</Carousel.Item>
				{/each}
			</Carousel.Content>
			<Carousel.Previous />
			<Carousel.Next />
			<Carousel.Dots use_countdown_dots={{ active: true, delay: 4000 }} />
		</Carousel.Root>
	</div>
</section>
