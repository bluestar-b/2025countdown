<script>
	let days = $state(0);
	let hours = $state(0);
	let minutes = $state(0);
	let seconds = $state(0);
	let isCountdownComplete = $state(false);

	function getTargetTime() {
		return new Date('2025-01-01T00:00:00');
	}

	function updateCountdown() {
		const now = new Date(); // User's local time
		const targetDate = getTargetTime();
		const diff = targetDate - now;

		if (diff <= 0) {
			isCountdownComplete = true;
			days = hours = minutes = seconds = 0;
		} else {
			isCountdownComplete = false;
			days = Math.floor(diff / (1000 * 60 * 60 * 24));
			hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
			minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
			seconds = Math.floor((diff % (1000 * 60)) / 1000);
		}
	}

	$effect(() => {
		updateCountdown();
		const interval = setInterval(updateCountdown, 1000);
		return () => clearInterval(interval);
	});
</script>

<div class="snowflakes" aria-hidden="true">
	<div class="snowflake">
		<div class="inner">❅</div>
	</div>
	<div class="snowflake">
		<div class="inner">❅</div>
	</div>
	<div class="snowflake">
		<div class="inner">❅</div>
	</div>
	<div class="snowflake">
		<div class="inner">❅</div>
	</div>
	<div class="snowflake">
		<div class="inner">❅</div>
	</div>
	<div class="snowflake">
		<div class="inner">❅</div>
	</div>
	<div class="snowflake">
		<div class="inner">❅</div>
	</div>
	<div class="snowflake">
		<div class="inner">❅</div>
	</div>
	<div class="snowflake">
		<div class="inner">❅</div>
	</div>
	<div class="snowflake">
		<div class="inner">❅</div>
	</div>
	<div class="snowflake">
		<div class="inner">❅</div>
	</div>
	<div class="snowflake">
		<div class="inner">❅</div>
	</div>
</div>

<div class="mx-auto w-full max-w-md p-6 text-white">
	<div class="mb-6">
		<h2 class="mb-2 text-center text-2xl font-bold text-gray-100">
			{isCountdownComplete ? 'Happy New Year!' : 'Countdown to 2025'}
		</h2>
		<p class="text-center text-gray-400">
			{isCountdownComplete ? 'Welcome to the Future!' : 'Time left until the New Year'}
		</p>
	</div>
	<div class="mb-6 grid grid-cols-4 gap-4 text-center">
		<div class="flex flex-col items-center rounded-lg bg-gray-900 p-4">
			<span class="text-4xl font-bold text-gray-100 md:text-5xl">{days}</span>
			<span class="text-sm text-gray-400">DAYS</span>
		</div>
		<div class="flex flex-col items-center rounded-lg bg-gray-900 p-4">
			<span class="text-4xl font-bold text-gray-100 md:text-5xl">{hours}</span>
			<span class="text-sm text-gray-400">HOURS</span>
		</div>
		<div class="flex flex-col items-center rounded-lg bg-gray-900 p-4">
			<span class="text-4xl font-bold text-gray-100 md:text-5xl">{minutes}</span>
			<span class="text-sm text-gray-400">MINUTES</span>
		</div>
		<div class="flex flex-col items-center rounded-lg bg-gray-900 p-4">
			<span class="text-4xl font-bold text-gray-100 md:text-5xl">{seconds}</span>
			<span class="text-sm text-gray-400">SECONDS</span>
		</div>
	</div>
</div>
