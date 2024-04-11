<script>
	import '../app.css';
</script>

<div class="flex h-screen flex-col justify-between">
	<header class="h-10 bg-red-500">Header</header>
	<div class="container mx-auto mb-auto h-10 bg-green-500"><slot /></div>
	<footer class="h-10 bg-blue-500">Footer</footer>
</div>
