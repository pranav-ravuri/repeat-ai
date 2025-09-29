<script lang="ts">
	import clsx from 'clsx';

	let tag = $state<'section' | 'div' | 'main'>('section');

	let { children, ...restProps } = $props();
</script>

<svelte:element
	this={tag}
	{...restProps}
	class={clsx('px-4 py-14 first:pt-10 md:px-6 md:py-20 lg:py-24', restProps['class'])}
>
	<div class="mx-auto flex w-full max-w-6xl flex-col items-center">
		{@render children()}
	</div>
</svelte:element>
