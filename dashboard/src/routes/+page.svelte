<script>
	import { onMount } from 'svelte';

	let multiSellerData = $state([]);

	onMount(async () => {
		const res = await fetch('/data/multi_seller.json');
		multiSellerData = await res.json();
	});

	const fmt = (n) => `${(n * 100).toFixed(1)}%`;
</script>

<article>
	<p class="text-xs font-medium uppercase tracking-widest text-neutral-500 mb-4">
		Finding 1 of 3 · The Counterintuitive One
	</p>

	<h1 class="text-4xl md:text-5xl font-bold leading-tight tracking-tight mb-6 max-w-2xl">
		Multi-seller orders aren't a logistics problem. They're a
		<span class="text-amber-400">3.6×</span> dissatisfaction problem.
	</h1>

	<p class="text-lg leading-relaxed text-neutral-300 mb-12 max-w-2xl">
		Conventional wisdom: orders with multiple sellers must arrive late and disorganized, which is
		why customers leave bad reviews. The data disagrees — multi-seller orders are actually
		<span class="text-white font-medium">faster</span> and
		<span class="text-white font-medium">more on-time</span> than single-seller orders. They still
		get 4* more 1-star reviews.
	</p>

	<section class="mb-12">
		<h2 class="text-lg font-semibold mb-4">The data</h2>
		<div class="rounded-lg bg-neutral-900 border border-neutral-800 shadow-md overflow-hidden">
			<table class="w-full text-sm">
				<thead class="bg-neutral-900 border-b border-neutral-800">
					<tr class="text-neutral-400 text-left">
						<th class="px-5 py-3 font-medium">Sellers / order</th>
						<th class="px-5 py-3 font-medium text-right">Orders</th>
						<th class="px-5 py-3 font-medium text-right">1-star rate</th>
						<th class="px-5 py-3 font-medium text-right">Late rate</th>
						<th class="px-5 py-3 font-medium text-right">Avg days</th>
					</tr>
				</thead>
				<tbody>
					{#each multiSellerData as row}
						<tr class="border-b border-neutral-800/50 last:border-0">
							<td class="px-5 py-3 font-medium">{row.unique_sellers}</td>
							<td class="px-5 py-3 text-right text-neutral-300"
								>{row.n_orders.toLocaleString()}</td
							>
							<td
								class="px-5 py-3 text-right font-semibold {row.star_1_rate > 0.15
									? 'text-red-400'
									: row.star_1_rate < 0.1
										? 'text-emerald-400'
										: 'text-amber-400'}"
							>
								{fmt(row.star_1_rate)}
							</td>
							<td class="px-5 py-3 text-right text-neutral-300">{fmt(row.late_rate)}</td>
							<td class="px-5 py-3 text-right text-neutral-300"
								>{row.avg_delivery_days.toFixed(1)}</td
							>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
		<p class="mt-3 text-xs text-neutral-500">
			Source: 95,809 delivered orders with reviews. Buckets with fewer than 50 orders excluded.
		</p>
	</section>

	<section class="mb-12">
		<h2 class="text-lg font-semibold mb-4">So what's actually happening?</h2>
		<p class="text-neutral-300 leading-relaxed mb-4">
			Three hypotheses worth testing: <span class="text-white font-medium">fragmented arrivals</span>
			create uncertainty even when each shipment is on time;
			<span class="text-white font-medium">quality variance across sellers</span>
			means one bad item tanks the whole order;
			<span class="text-white font-medium">customers don't expect</span> their order to come from multiple
			sellers and feel ambushed when it does.
		</p>
		<p class="text-neutral-400 text-sm">
			Chi-square test of independence confirms the association is real:
			<span class="font-mono text-neutral-300">χ² = 991, p &lt; 0.001, OR = 5.4</span>.
		</p>
	</section>

	<section
		class="mb-12 rounded-lg border-l-2 border-amber-400 bg-neutral-900 shadow-md p-6"
	>
		<h2 class="text-lg font-semibold mb-3">Recommendation</h2>
		<p class="text-neutral-300 mb-4">
			Multi-seller orders are 1.3% of volume but a disproportionate share of dissatisfaction.
			Highest-leverage interventions:
		</p>
		<ul class="list-disc list-outside pl-5 space-y-2 text-neutral-300 marker:text-neutral-600">
			<li>
				Set explicit expectations at checkout:
				<em class="text-neutral-200">"Your order will arrive in 2 shipments."</em>
			</li>
			<li>Trigger a unified status view for multi-seller orders so customers see one timeline.</li>
			<li>A/B test whether bundling at the warehouse (single shipment) reduces 1-star rates.</li>
		</ul>
	</section>

	<nav class="pt-8 border-t border-neutral-900">
		<a
			href="/delivery"
			class="text-neutral-300 hover:text-white transition-colors text-sm font-medium"
		>
			Next: the delivery cliff →
		</a>
	</nav>
</article>