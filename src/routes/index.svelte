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
		'👦👴🚗⏱': ['back to the future'],
		'👸🌹🐻': ['beauty and the beast'],
		'🌃🇫🇷🗼': ['midnight in paris', 'a midnight in paris'],
		'👸🐸👑': ['princess and the frog', 'the princess and the frog'],
		'5️⃣0️⃣0️⃣☀️❤️': ['500 days of summer'],
		'👨🏻👨🏻❤️🗻': ['brokeback mountain'],
		'🐳➡🌊': ['free willy'],
		'⚡️👦🔨': ['thor'],
		'👨🏻🎤': ['bohemian rhapsody'],
		'🐼👊': ['kung fu panda'],
		'👦💍➡️🌋': ['lord of the rings', 'the lord of the rings'],
		'👽📞👦🚲🌕': ['et', 'E.T. the Extra-Terrestrial'],
		'🍴🙏❤️': ['eat, pray, love'],
		'👑💬🎙': ['the king\'s speech', 'king\'s speech', 'kings speech'],
		'🐍✈️': ['snakes on a plane'],
		'🐛🐜🐞': ['a bug\'s life', "bugs life", 'bug\'s life'],
		'📱🍎': ['jobs'],
		'⏰🔧🍊': ['a clockwork orange', 'clockwork orange'],
		'💍📺': ['the ring', 'ring'],
		'👦✂️🙌': ['edward scissorhands'],
		'🌍🙈🙊🙉': ['planet of the apes', 'the planet of the apes'],
		'👦🍫🏭': ['charlie and the chocolate factory'],
		'🛳🧊': ['titanic']
	};

	let random_keys = [' '];

	function foo() {
		random_keys = shuffle(Object.keys(movies));
	}

	let [index, answer, guess] = [0, undefined, ""];

	function submit_guess() {
		const my_guess = guess.toLowerCase().trim();
		answer = movies[random_keys[index]].includes(my_guess);
		console.log(my_guess, answer);
		if (answer === true) {
			[guess, index] = ['', index + 1];
		}
	}
	function handleClick() {
		[guess, index, answer] = ['', index + 1, true];
	}
</script>

<main
	class="flex flex-col items-center justify-center min-h-screen text-center bg-gray-50"
	on:loadeddata={foo()}
>
	{#if index === random_keys.length}
		<h1 class="m-2 text-8xl py-7 md:text-8xl text-green-600">You win! 🎉</h1>
	{:else}
		<h1 class="m-2 font-semibold md:text-7xl text-4xl py-7 bg-clip-text text-transparent bg-gradient-to-l from-pink-500 via-red-500 to-yellow-500">Guess the movie</h1>

		<h1 class="m-2 text-5xl py-7 tracking-[0.2em] md:text-9xl">{random_keys[index]}</h1>
		<div class="flex item-center px-8 mt-10">
			<form on:submit|preventDefault={submit_guess}>
				<input
					bind:value={guess}
					placeholder="Which movie?"
					class="p-2 text-center bg-gray-100 text-gray-600 m-2 rounded-xl shadow-md"
				/>
				<button class="px-8 p-2 hover:pt-2 text-white bg-gradient-to-l from-pink-500 via-red-500 to-yellow-500 hover:from-red-500 
				rounded-xl shadow-md">Guess</button>
			</form>
		</div>
		<div class="m-8 p-1">
			<p class="text-gray-600">You have guessed {index}/{random_keys.length}</p>
			{#if answer == undefined}
				<p class="text-gray-600">You can do it 💪</p>
			{:else if answer == true}
				<p class="text-green-600">Correct ☑️</p>
			{:else if answer == false}
				<button class="text-red-600" on:click="{handleClick}">I give up🤦‍♂ ️Skip to next movie.</button>
			{/if}
		</div>
	{/if}
</main>
