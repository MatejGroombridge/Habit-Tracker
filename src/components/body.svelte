<script>
	import { each } from 'svelte/internal';

	$: habitList = [
		{
			name: 'Example Habit',
			days: 69,
			completed: false
		}
	];

	let userName = 'Matej';
	let newHabit = '';
	let streakNum = 0;
	let highestStreakCurrent = 0;
	let highestStreakAllTime = 0;

	function addToList() {
		if (newHabit === '') {
			return;
		}
		habitList = [...habitList, { name: newHabit, days: 0, completed: false }];
		newHabit = '';

		updateStats();
	}

	function removeFromList(index) {
		habitList.splice(index, 1);
		habitList = habitList;

		updateStats();
	}

	function markAsComplete(habit) {
		habit.completed = true;
		habit.days += 1;
		habitList = habitList;

		updateStats();
	}

	function updateStats() {
		let streak = 0;
		let currentStreak = 0;
		let allTimeStreak = 0;

		habitList.forEach((habit) => {
			if (habit.days > 0) {
				streak += 1;
			}

			if (habit.days > currentStreak) {
				currentStreak = habit.days;
			}
		});

		streakNum = streak;
		highestStreakCurrent = currentStreak;

		if (highestStreakAllTime < highestStreakCurrent) {
			highestStreakAllTime = highestStreakCurrent;
		}
	}
</script>

<div class="wrapper left">
	<div class="container stats">
		<h2 class="welcome">Welcome Back <span class="user-name">{userName}</span>!</h2>
		<div class="streak-stats">
			<div class="info">
				<div class="streak-num">{streakNum}</div>
				<p>Current Streaks</p>
			</div>
			<div class="info">
				<div class="streak-num">{highestStreakCurrent}</div>
				<p>Highest: Current</p>
			</div>
			<div class="info">
				<div class="streak-num">{highestStreakAllTime}</div>
				<p>Highest: All Time</p>
			</div>
		</div>
	</div>

	<div class="container input">
		<h2>New Habit:</h2>
		<div class="half">
			<input class="half-size" bind:value={newHabit} type="text" maxlength="30" />
			<div on:click={addToList} class="btn half-size">ADD</div>
		</div>
	</div>
</div>

<div class="wrapper right">
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
				</div>
			</div>
		{/each}
	</div>

	<div class="view-all">
		<button class="sml-btn">View All</button>
	</div>
</div>
