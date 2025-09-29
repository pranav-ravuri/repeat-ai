<script lang="ts">
	let { children } = $props();
</script>

<em class="bg-gradient-to-b from-yellow-100 to-yellow-500 bg-clip-text text-transparent not-italic">
	{@render children()}
</em>
