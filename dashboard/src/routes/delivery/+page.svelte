<script>
	import { onMount } from 'svelte';

	let delayData = $state([]);

	onMount(async () => {
		const res = await fetch('/data/delivery_delay.json');
		delayData = await res.json();
	});

	const fmt = (n) => `${(n * 100).toFixed(1)}%`;

	const barColor = (rate) => {
		if (rate > 0.4) return 'bg-red-500';
		if (rate > 0.15) return 'bg-amber-500';
		return 'bg-emerald-500';
	};
</script>

<article>
	<p class="text-xs font-medium uppercase tracking-widest text-neutral-500 mb-4">
		Finding 2 of 3 · The Cliff
	</p>

	<h1 class="text-4xl md:text-5xl font-bold leading-tight tracking-tight mb-6 max-w-2xl">
		The moment a delivery goes late, customer sentiment falls off a
		<span class="text-red-400">cliff</span>.
	</h1>

	<p class="text-lg leading-relaxed text-neutral-300 mb-12 max-w-2xl">
		Orders arriving on-time or early get a 1-star review about 8% of the time — close to the
		baseline. The instant delivery slips past the promised date, the rate jumps to 41%. More than a
		week late, it hits <span class="text-red-400 font-semibold">70%</span>.
	</p>

	<section class="mb-12">
		<h2 class="text-lg font-semibold mb-4">1-star rate by delivery delay</h2>
		<div class="rounded-lg bg-neutral-900 border border-neutral-800 shadow-md p-6">
			<div class="space-y-3">
				{#each delayData as row}
					<div class="grid grid-cols-[1fr_2fr_auto] gap-4 items-center text-sm">
						<div class="text-neutral-300 font-medium">{row.delay_bucket}</div>
						<div class="bg-neutral-800 rounded h-8 overflow-hidden relative">
							<div
								class="h-full {barColor(row.star_1_rate)} flex items-center justify-end pr-2 transition-all duration-500"
								style="width: {row.star_1_rate * 100}%"
							>
								<span class="text-white text-xs font-semibold">{fmt(row.star_1_rate)}</span>
							</div>
						</div>
						<div class="text-neutral-500 text-xs whitespace-nowrap">
							n = {row.n_orders.toLocaleString()}
						</div>
					</div>
				{/each}
			</div>
		</div>
		<p class="mt-3 text-xs text-neutral-500">
			The discontinuity at the "on time" threshold suggests customers anchor strongly on the
			promised date.
		</p>
	</section>

	<section class="mb-12">
		<h2 class="text-lg font-semibold mb-4">The effect size</h2>
		<p class="text-neutral-300 leading-relaxed mb-4">
			Late-delivered orders have <span class="text-red-400 font-semibold">16× the odds</span> of
			receiving a 1-star review compared to on-time orders. This is by far the strongest factor
			identified — about 3× stronger than the multi-seller effect.
		</p>
		<p class="text-neutral-400 text-sm font-mono">
			χ² = 14,990, p &lt; 0.001, OR = 16.35
		</p>
	</section>

	<section class="mb-12 rounded-lg border-l-2 border-red-400 bg-neutral-900 shadow-md p-6">
		<h2 class="text-lg font-semibold mb-3">Recommendation</h2>
		<p class="text-neutral-300 mb-4">
			Late delivery is the single highest-leverage intervention target. Two specific moves:
		</p>
		<ul class="list-disc list-outside pl-5 space-y-3 text-neutral-300 marker:text-neutral-600">
			<li>
				<span class="text-white font-medium">Pad delivery estimates conservatively.</span> Olist already
				does this for most orders (median delivery is 12 days <em>before</em> estimate). The 6.7% of
				orders that still go late produce the bulk of dissatisfaction.
			</li>
			<li>
				<span class="text-white font-medium">Proactive comms when delays are predicted.</span> If a
				shipment looks like it'll miss the estimate, notify the customer before the date passes.
			</li>
		</ul>
	</section>

	<nav class="pt-8 border-t border-neutral-900">
		<a
			href="/summary"
			class="text-neutral-300 hover:text-white transition-colors text-sm font-medium"
		>
			Next: how all the findings fit together →
		</a>
	</nav>
</article>