<script>
	import '../app.css';
</script>

<div class="flex h-screen flex-col justify-between">
	<header class="bg-blue-500 dark:bg-orange-500">Header</header>
	<div class="container mx-auto mb-auto bg-blue-500 dark:bg-orange-500"><slot /></div>
	<footer class="bg-blue-500 dark:bg-orange-500">Footer</footer>
</div>
