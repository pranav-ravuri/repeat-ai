<script lang="ts">
	import Bounded from '$lib/components/Bounded.svelte';
	import type { Content } from '@prismicio/client';
	import { PrismicRichText, type SliceComponentProps } from '@prismicio/svelte';

	type Props = SliceComponentProps<Content.RichTextSlice>;

	const { slice }: Props = $props();
</script>

<Bounded>
	<div class="prose prose-lg prose-slate prose-invert w-full">

		<PrismicRichText field={slice.primary.content} />
	</div>
</Bounded>
