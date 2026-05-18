<script>
	const findings = [
		{
			name: 'Late delivery',
			effect: 'OR = 16.35',
			strength: 'Very strong',
			rate: '53.8% vs 6.6%',
			accent: 'border-red-400'
		},
		{
			name: 'Multi-seller orders',
			effect: 'OR = 5.40',
			strength: 'Strong',
			rate: '36.0% vs 9.4%',
			accent: 'border-amber-400'
		},
		{
			name: 'Product category',
			effect: "Cramér's V = 0.062",
			strength: 'Weak but real',
			rate: '~20% (worst) to ~3% (best)',
			accent: 'border-neutral-600'
		}
	];
</script>

<article>
	<p class="text-xs font-medium uppercase tracking-widest text-neutral-500 mb-4">
		Finding 3 of 3 · Summary
	</p>

	<h1 class="text-4xl md:text-5xl font-bold leading-tight tracking-tight mb-6 max-w-2xl">
		Three drivers, ranked by impact.
	</h1>

	<p class="text-lg leading-relaxed text-neutral-300 mb-12 max-w-2xl">
		Most analyses confirm what stakeholders already suspect. This one found that the obvious answer —
		<em>"multi-seller orders are slow"</em> — was wrong, and quantified just how much delivery delay
		matters relative to everything else.
	</p>

	<section class="mb-12 space-y-3">
		{#each findings as f}
			<div
				class="rounded-lg bg-neutral-900 border border-neutral-800 shadow-md border-l-2 {f.accent} p-5"
			>
				<h3 class="font-semibold text-base mb-1">{f.name}</h3>
				<p class="text-sm text-neutral-400 mb-2">{f.strength}</p>
				<p class="text-xs text-neutral-500 font-mono">
					{f.effect} · 1-star rate: {f.rate}
				</p>
			</div>
		{/each}
	</section>

	<section class="mb-12">
		<h2 class="text-lg font-semibold mb-4">What this means for Olist (or any e-commerce platform)</h2>
		<p class="text-neutral-300 leading-relaxed mb-4">
			If you only have engineering bandwidth for one intervention this quarter, invest it in
			reducing late deliveries. The next-best target is reducing multi-seller order friction — not
			by speeding up shipping (it's already fast) but by managing customer expectations and
			communications.
		</p>
		<p class="text-neutral-300 leading-relaxed">
			Product category is a useful segmentation lens but not an intervention target.
		</p>
	</section>

	<section class="mb-12">
		<h2 class="text-lg font-semibold mb-4">Caveats — what this analysis can't tell you</h2>
		<ul class="list-disc list-outside pl-5 space-y-3 text-neutral-300 marker:text-neutral-600">
			<li>
				<span class="text-white font-medium">Observational, not causal.</span> Late delivery
				<em>predicts</em>
				1-star reviews; whether it <em>causes</em> them requires a randomized intervention to confirm.
			</li>
			<li>
				<span class="text-white font-medium">Selection bias.</span> Findings apply to customers who chose
				to leave reviews.
			</li>
			<li>
				<span class="text-white font-medium">Brazilian e-commerce context.</span> Effect sizes likely
				generalize qualitatively but not quantitatively.
			</li>
		</ul>
	</section>

	<section class="pt-8 border-t border-neutral-900 text-sm text-neutral-500">
		<h2 class="text-lg font-semibold mb-3 text-neutral-300">Methodology</h2>
		<p>
			Chi-square tests of independence with effect sizes (odds ratios for 2×2, Cramér's V for
			larger tables). Pre-registered hypotheses written before formal tests to avoid p-hacking.
			Full notebook with code, decisions, and caveats:
			<a
				href="https://github.com/Justsharon/olist-review-drivers"
				target="_blank"
				class="text-neutral-300 hover:text-white transition-colors"
			>
				GitHub repo →
			</a>
		</p>
	</section>
</article>