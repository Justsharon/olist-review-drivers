<script>
	import '../app.css';
	import { page } from '$app/stores';
	let { children } = $props();
</script>

<div class="min-h-screen flex flex-col bg-neutral-950 text-neutral-100">
	<header class="sticky top-0 z-10 border-b border-neutral-900 bg-neutral-950/80 backdrop-blur-md">
		<div class="max-w-4xl mx-auto px-6 py-4 flex justify-between items-center">
			<a href="/" class="font-semibold text-sm tracking-tight text-white">
				olist · review drivers
			</a>
			<nav class="flex gap-6 text-sm">
				<a
					href="/"
					class="transition-colors {$page.url.pathname === '/'
						? 'text-white'
						: 'text-neutral-500 hover:text-neutral-200'}"
				>
					The Surprise
				</a>
				<a
					href="/delivery"
					class="transition-colors {$page.url.pathname === '/delivery'
						? 'text-white'
						: 'text-neutral-500 hover:text-neutral-200'}"
				>
					Delivery Cliff
				</a>
				<a
					href="/summary"
					class="transition-colors {$page.url.pathname === '/summary'
						? 'text-white'
						: 'text-neutral-500 hover:text-neutral-200'}"
				>
					Summary
				</a>
			</nav>
		</div>
	</header>

	<main class="flex-1 max-w-3xl w-full mx-auto px-6 py-16">
		{@render children()}
	</main>

	<footer class="border-t border-neutral-900 py-8 text-center text-sm text-neutral-500">
		<p>
			Analysis of 95,809 delivered Brazilian e-commerce orders. ·
			<a
				href="https://github.com/Justsharon/olist-review-drivers"
				target="_blank"
				class="text-neutral-300 hover:text-white transition-colors"
			>
				View on GitHub →
			</a>
		</p>
	</footer>
</div>


