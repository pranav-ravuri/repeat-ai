<script lang="ts">
	import Bounded from '$lib/components/Bounded.svelte';
	import background from './background.jpg';
	import type { Content } from '@prismicio/client';
	import { PrismicRichText, PrismicText, type SliceComponentProps } from '@prismicio/svelte';
	import LogoBackground from './LogoBackground.svelte';
	import StylizedLogoMark from './StylizedLogoMark.svelte';
	import clsx from 'clsx';
	import IconCloudflare from './icons/IconCloudflare.svelte';
	import IconDigitalocean from './icons/IconDigitalocean.svelte';
	import IconFigma from './icons/IconFigma.svelte';
	import IconFly from './icons/IconFly.svelte';
	import IconGithub from './icons/IconGithub.svelte';
	import IconNpm from './icons/IconNpm.svelte';

	type Props = SliceComponentProps<Content.IntegrationsSlice>;

	const { slice }: Props = $props();

	const icons = {
		digitalocean: IconDigitalocean,
		cloudflare: IconCloudflare,
		github: IconGithub,
		fly: IconFly,
		figma: IconFigma,
		npm: IconNpm
	} as const;

	const integrations = slice.primary.integrations.map((item) => ({
		...item,
		component: icons[item.icon as keyof typeof icons] ?? null
	}));
</script>

<Bounded
	data-slice-type={slice.slice_type}
	data-slice-variation={slice.variation}
	class="relative overflow-hidden"
>
	<img src={background} alt="" class="absolute inset-0 h-full w-full object-cover" />

	<LogoBackground />
	<div class="relative">
		<h2
			class="mx-auto max-w-2xl bg-gradient-to-b from-violet-50 to-violet-300 bg-clip-text py-2 text-center text-5xl font-medium text-balance text-transparent md:text-7xl"
		>
			<PrismicText field={slice.primary.heading} />
		</h2>

		<div class="mx-auto mt-6 max-w-md text-center text-balance text-gray-300">
			<PrismicRichText field={slice.primary.body} />
		</div>

		<div class="mt-20 flex flex-col items-center justify-center md:flex-row">
			{#each integrations as item, index}
				{#if item.icon}
					{#if index === Math.floor(slice.primary.integrations.length / 2)}
						<StylizedLogoMark />
						<div class="signal-line rotate-180"></div>
					{/if}

					<div
						class="pulsing-icon max-w max-h flex aspect-square shrink-0 items-center justify-center rounded-full border border-violet-50/30 bg-violet-50/25 p-3 text-3xl text-violet-100 opacity-40 md:text-3xl lg:text-5xl"
					>
						<item.component class="w-10 text-3xl md:text-3xl lg:text-5xl" />
					</div>

					{#if index !== slice.primary.integrations.length - 1}
						<div
							class={clsx(
								'signal-line',
								index >= Math.floor(slice.primary.integrations.length / 2)
									? 'rotate-180'
									: 'rotate-0'
							)}
						></div>
					{/if}
				{/if}
			{/each}
		</div>
	</div>
</Bounded>
