<script>
	import { each } from 'svelte/internal';

	let habits = [
		{
			name: 'Go for a run',
			days: 91
		},
		{
			name: 'Read 10 pages',
			days: 56
		},
		{
			name: 'Play the French Horn',
			days: 2
		},
		{
			name: 'Sup',
			days: 7
		}
	];
</script>

<div class="container output">
	<div class="sml-btn">View All</div>
	{#each habits as habit}
		<div class="habit">
			<div class="text">
				<h3>{habit.name}</h3>
				<p>🔥 {habit.days} day streak</p>
			</div>
			<div class="options">Hello</div>
		</div>
	{/each}
</div>
