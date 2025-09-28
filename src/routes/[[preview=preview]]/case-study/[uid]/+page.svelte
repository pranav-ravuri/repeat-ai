<script lang="ts">
	import { PrismicImage, PrismicText, SliceZone } from '@prismicio/svelte';

	import { components } from '$lib/slices';
	import type { PageProps } from './$types';
	import Bounded from '$lib/components/Bounded.svelte';
	import TriangleGrid from '$lib/components/TriangleGrid.svelte';

	const { data }: PageProps = $props();
	console.log('🚀 ~ data:', data);
</script>

<Bounded>
	<div class="relative grid w-full place-items-center text-center">
		<TriangleGrid />

		<h1 class="text5xl font-medium md:text-7xl">
			<PrismicText field={data.page.data.company} />
			<span class="text-lg text-yellow-500 block">Case Study</span>
		</h1>

		<p class="mt-8 mb-4 max-w-xl text-lg text-slate-300">
			<PrismicText field={data.page.data.description} />
		</p>

    <PrismicImage field={data.page.data.image} class="logo-image rounded-lg opacity-100"/>
	</div>
	<div class="mx-auto mt-12 md:mt-16">
		<SliceZone slices={data.page.data.slices} {components} />
	</div>
</Bounded>
