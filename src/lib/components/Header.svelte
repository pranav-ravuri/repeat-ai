<script lang="ts">
	import { PrismicLink } from '@prismicio/svelte';
	import WordMark from './WordMark.svelte';
	import ButtonLink from './ButtonLink.svelte';

	import type { Content } from '@prismicio/client';
	import { asLink } from '@prismicio/client';
	import clsx from 'clsx';
	import IconClose from './icons/IconClose.svelte';
	import IconMenu from './icons/iconMenu.svelte';
	import { page } from '$app/state';

	import type { LinkField } from '@prismicio/client';

	type Props = {
		settings: Content.SettingsDocument;
	};
	const { settings }: Props = $props();

	let isOpen = $state(false);
	const toggleOpen = $derived(() => (isOpen = !isOpen));
	const close = $derived(() => (isOpen = false));

	const isActive = (link: LinkField) => {
		const path = asLink(link);
		return path && page.url.pathname.includes(path);
	};
</script>

<header class="p-4 md:p-6">
	<nav
		class="mx-auto flex max-w-6xl flex-col justify-between py-2 font-medium text-white md:flex-row md:items-center"
		aria-label="Main"
	>
		<div class="flex items-center justify-between">
			<a href="/" onclick={close} class="z-50">
				<WordMark />
				<span class="sr-only">{settings.data.site_title} home page</span>
			</a>

			<button
				aria-expanded={isOpen}
				type="button"
				class="block p-2 text-3xl text-white md:hidden"
				onclick={toggleOpen}
			>
				<IconMenu />
			</button>
		</div>

		<!-- Nobile Nav -->

		<div
			class={clsx(
				'fixed inset-0 z-40 flex flex-col items-end bg-gray-950 pt-6 pr-4 transition-transform duration-300 ease-in-out md:hidden',
				isOpen ? 'translate-x-0' : 'translate-x-[100%]'
			)}
		>
			<button
				aria-expanded={isOpen}
				type="button"
				class="block p-2 text-3xl text-white md:hidden"
				onclick={toggleOpen}
			>
				<IconClose />
			</button>

			<ul class="grid justify-items-end gap-8">
				{#each settings.data.navigation as item (item.label)}
					<li>
						{#if item.cta_button}
							<ButtonLink field={item.link} onclick={close} aria-current={isActive(item.link) ? 'page' : undefined}>
								{item.label}
							</ButtonLink>
						{:else}
							<PrismicLink
								field={item.link}
								onclick={close}
								class=" block min-h-11 px-3 text-3xl first:mt-8"
								aria-current={isActive(item.link) ? 'page' : undefined}
							>
								{item.label}
							</PrismicLink>
						{/if}
					</li>
				{/each}
			</ul>
		</div>

		<!-- Desktop Nav -->

		<ul class="hidden gap-6 md:flex">
			{#each settings.data.navigation as item (item.label)}
				<li>
					{#if item.cta_button}
						<ButtonLink field={item.link} class="inline-flex min-h-11 items-center" aria-current={isActive(item.link) ? 'page' : undefined}>
							{item.label}
						</ButtonLink>
					{:else}
						<PrismicLink field={item.link} class="inline-flex min-h-11 items-center" aria-current={isActive(item.link) ? 'page' : undefined}>
							{item.label}
						</PrismicLink>
					{/if}
				</li>
			{/each}
		</ul>
	</nav>
</header>
