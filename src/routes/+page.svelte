<h1 class="myclass">Hello world!</h1>

<style>
	/* 
		Убеждаемся что lint @apply проходит без проблем
		https://github.com/tailwindlabs/tailwindcss/discussions/5258
	*/
	.myclass {
		@apply text-gray-500;
	}
</style>
