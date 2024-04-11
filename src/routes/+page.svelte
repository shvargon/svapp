<script>
	import { onMount } from 'svelte';
	import { themeChange } from 'theme-change';

	// NOTE: the element that is using one of the theme attributes must be in the DOM on mount
	onMount(() => {
		themeChange(false);
		// 👆 false parameter is required for svelte
	});
</script>

<h1 class="myclass">Hello world!</h1>
<button class="m-2 flex max-w-xs border p-4" data-toggle-theme="dark,light" data-act-class="dark">
	change theme
</button>

<style>
	:global(html) {
		@apply bg-gray-500;
	}

	:global(html[data-theme='dark']) {
		@apply bg-slate-300;
	}

	/* 
		Убеждаемся что lint @apply проходит без проблем
		https://github.com/tailwindlabs/tailwindcss/discussions/5258
	*/
	.myclass {
		@apply text-gray-500;
	}
</style>
