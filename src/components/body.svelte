<script>
	import { each } from 'svelte/internal';

	$: habitList = [
		{
			name: 'Example Habit',
			days: 69,
			completed: false
		}
	];

	let newHabit = '';

	function addToList() {
		if (newHabit === '') {
			return;
		}
		habitList = [...habitList, { name: newHabit, days: 0, completed: false }];
		newHabit = '';
	}

	function removeFromList(index) {
		habitList.splice(index, 1);
		habitList = habitList;
	}

	function markAsComplete(habit) {
		habit.completed = true;
		habit.days += 1;
		console.log('It worked!');
		habitList = habitList;
	}
</script>

<div class="container input">
	<h2>New Habit:</h2>
	<input bind:value={newHabit} type="text" maxlength="30" />
	<div on:click={addToList} class="btn">ADD</div>
</div>

<div class="container output">
	{#if habitList.length < 1}
		<h2>Nothing Here!</h2>
	{/if}
	{#each habitList as habit, index}
		<div class="habit">
			<div class="habit-text">
				<h3>{habit.name}</h3>
				{#if habit.days > 10}
					<p>🔥{habit.days} day streak</p>
				{:else}
					<p>{habit.days} day streak</p>
				{/if}
			</div>
			<div class="habit-btns">
				<a href="/" class="habit-btn done" on:click={() => markAsComplete(habit)}>
					<img src="tick-icon.png" alt="tick icon" />
				</a>
				<a href="/" class="habit-btn delete" on:click={() => removeFromList(index)}>
					<img src="bin-icon.png" alt="bin icon" />
				</a>
			</div>
		</div>
	{/each}
</div>

<div class="view-all">
	<button class="sml-btn">View All</button>
</div>
