<script>
	let days = $state(0);
	let hours = $state(0);
	let minutes = $state(0);
	let seconds = $state(0);
	let isCountdownComplete = $state(false);

	function getTimezoneOffset() {
		const urlParams = new URLSearchParams(window.location.search);
		return parseInt(urlParams.get('tz')) || 0;
	}

	function getCustomTargetTime() {
		const urlParams = new URLSearchParams(window.location.search);
		const targetParam = urlParams.get('target');
		return targetParam ? new Date(targetParam) : new Date('2025-01-01T00:00:00Z');
	}

	function updateCountdown() {
		const now = new Date();

		const targetDateUTC = getCustomTargetTime();

		const offset = getTimezoneOffset();
		const targetDate = new Date(targetDateUTC.getTime() + offset * 60 * 60 * 1000);

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

<div
	class="mx-auto w-full max-w-md overflow-hidden rounded-lg border-8 border-purple-600 bg-yellow-300 shadow-[10px_10px_0_0_rgba(0,0,0,0.3)]"
>
	<div class="bg-gradient-to-r from-cyan-400 to-blue-500 p-6">
		<h2 class="mb-2 animate-bounce text-center text-4xl font-bold text-red-600">
			{isCountdownComplete ? 'Happy New Year!' : 'Countdown to 2025!'}
		</h2>
		<p class="mb-4 animate-pulse text-center text-gray-900">
			{isCountdownComplete ? 'Welcome to the Future!' : 'Time left until the FUTURE!'}
		</p>

		<div class="grid grid-cols-2 gap-4 text-center">
			<div
				class="flex rotate-2 transform flex-col rounded-lg border-4 border-green-500 bg-pink-400 p-2"
			>
				<span class="text-5xl font-bold text-white">{isCountdownComplete ? '0' : days}</span>
				<span class="text-sm text-yellow-400">DAYS</span>
			</div>
			<div
				class="flex -rotate-2 transform flex-col rounded-lg border-4 border-pink-500 bg-green-400 p-2"
			>
				<span class="text-5xl font-bold text-white">{isCountdownComplete ? '0' : hours}</span>
				<span class="text-sm text-purple-700">HOURS</span>
			</div>
			<div
				class="flex rotate-2 transform flex-col rounded-lg border-4 border-yellow-500 bg-purple-400 p-2"
			>
				<span class="text-5xl font-bold text-white">{isCountdownComplete ? '0' : minutes}</span>
				<span class="text-sm text-green-600">MINUTES</span>
			</div>
			<div
				class="flex -rotate-2 transform flex-col rounded-lg border-4 border-blue-500 bg-orange-400 p-2"
			>
				<span class="text-5xl font-bold text-white">{isCountdownComplete ? '0' : seconds}</span>
				<span class="text-sm text-red-600">SECONDS</span>
			</div>
		</div>
	</div>
	<!-- svelte-ignore a11y_distracting_elements -->
	<marquee class="bg-black py-2 text-white" scrollamount="10">
		{isCountdownComplete ? 'HAPPY NEW YEAR!!! 🎉🎉🎉' : 'GET READY FOR 2025!!!!!!!!!'}
	</marquee>
</div>

