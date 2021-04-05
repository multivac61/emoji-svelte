<script context="module">
	export const prerender = true;
</script>

<script>
	function shuffle(array) {
		for (var i = 0; i < array.length - 1; i++) {
			const j = i + Math.floor(Math.random() * (array.length - i));
			[array[i], array[j]] = [array[j], array[i]];
		}
		return array;
	}
	const movies = {
		'👦👴🚗⏱': 'back to the future',
		'👸🌹🐻': 'beauty and the beast',
		'🌃🇫🇷🗼': 'midnight in paris',
		'👸🐸👑': 'princess and the frog',
		'5️⃣0️⃣0️⃣☀️❤️': '500 days of summer',
		'👨🏻👨🏻❤️🗻': 'brokeback mountain',
		'🐳➡🌊': 'free willy',
		'⚡️👦🔨': 'thor',
		'👨🏻🎤': 'bohemian rhapsody',
		'🐼👊': 'kung fu panda',
		'👦💍➡️🌋': 'the lord of the rings',
		'👽📞👦🚲🌕': 'et',
		'🍴🙏❤️': 'eat, pray, love',
		'👑💬🎙': "the king's speech",
		'🐍✈️': 'snakes on a plane',
		'🐛🐜🐞': "a bug's life",
		'📱🍎': 'jobs',
		'⏰🔧🍊': 'a clockwork orange',
		'💍📺': 'the ring',
		'👦✂️🙌': 'edward scissorhands',
		'🌍🙈🙊🙉': 'planet of the apes',
		'👦🍫🏭': 'charlie and the chocolate factory',
		'🛳🧊': 'titanic'
	};

	let random_keys = shuffle(Object.keys(movies));

	let [guess, answer, index] = ['', undefined, 0];

	function submit_guess() {
		answer = guess.toLowerCase().trim() === movies[random_keys[index]];
		if (answer === true) {
			[guess, index] = ['', index + 1];
		}
	}
</script>

<main class="flex flex-col items-center justify-center min-h-screen text-center">
	{#if index === random_keys.length}
		<h1 class="m-2 text-8xl py-7 md:text-8xl text-green-600">You win! 🎉</h1>
	{:else}
		<h1 class="m-2 text-3xl py-7 md:text-6xl">Guess the 🎞</h1>
		<h1 class="m-2 text-5xl py-7 tracking-[0.2em] md:text-9xl ">{random_keys[index]}</h1>
		<div class="flex item-center px-8 mt-10 text-gray-700">
			<form on:submit|preventDefault={submit_guess}>
				<input
					bind:value={guess}
					placeholder="Which movie?"
					class="p-2 text-center bg-gray-100 text-gray-600 m-2"
				/>
				<button class="px-8 p-2 text-xl font-bold">Guess</button>
			</form>
		</div>
		<div class="m-8 p-1">
			{#if answer == undefined}
				<p class="text-gray-600">You can do it 💪</p>
				<p class="text-white">!</p>
			{:else if answer == true}
				<p class="text-green-600">Correct ☑️</p>
				<p class="text-gray-200">Now try this one 🙈</p>
			{:else}
				<p class="text-red-600">Incorrect 🚽</p>
				<p class="text-gray-200">Try Again...</p>
			{/if}
		</div>
	{/if}
</main>
