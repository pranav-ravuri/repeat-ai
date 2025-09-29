<script lang="ts">
	let { children } = $props();
</script>

<h2 class="max-w-3xl text-center text-5xl font-medium text-balance md:text-7xl">
	{@render children()}
</h2>
