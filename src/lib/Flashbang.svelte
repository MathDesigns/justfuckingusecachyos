<script lang="ts">
	import catLaugh from '$lib/assets/catlaugh.jpg';

	let isFlashing = $state(false);
	let showInsult = $state(false);

	function playFlashbangSound() {
		const audio = new Audio('/flashbang.mp3');
		audio.volume = 0.1; 
		audio.play().catch((e) => console.error("Audio failed:", e));
	}

    function playMockerySound() {
        const audio = new Audio('/mockery.mp3');
        audio.volume = 0.1;
        audio.play().catch((e) => console.error("Audio failed:", e));
    }

	function triggerFlashbang() {
		playFlashbangSound();
		isFlashing = true;
		showInsult = false; 

		// 1. Instant Whiteout 
		setTimeout(() => {
			// 2. Start recovering vision 
			isFlashing = false;
			
			// 3. Show the insult + Play Second Sound
			setTimeout(() => {
				showInsult = true;
                playMockerySound(); // <--- Trigger the second sound here
				
				// 4. Hide insult after 6 seconds
				setTimeout(() => {
					showInsult = false;
				}, 3200);
			}, 400); 
		}, 150); 
	}
</script>

<button
	onclick={triggerFlashbang}
	class="fixed top-6 right-6 z-40 bg-gray-800 hover:bg-gray-700 text-yellow-400 p-3 rounded-full border border-gray-600 transition-all hover:scale-110 active:scale-95 shadow-lg cursor-pointer group"
	aria-label="Toggle Light Mode"
	title="Switch to Light Mode"
>
	<svg
		xmlns="http://www.w3.org/2000/svg"
		width="24"
		height="24"
		viewBox="0 0 24 24"
		fill="none"
		stroke="currentColor"
		stroke-width="2"
		stroke-linecap="round"
		stroke-linejoin="round"
		class="group-hover:rotate-45 transition-transform duration-500"
	>
		<circle cx="12" cy="12" r="5"></circle>
		<line x1="12" y1="1" x2="12" y2="3"></line>
		<line x1="12" y1="21" x2="12" y2="23"></line>
		<line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
		<line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
		<line x1="1" y1="12" x2="3" y2="12"></line>
		<line x1="21" y1="12" x2="23" y2="12"></line>
		<line x1="4.22" y1="19.78" x2="5.64" y2="18.36"></line>
		<line x1="18.36" y1="5.64" x2="19.78" y2="4.22"></line>
	</svg>
</button>

<div
	class="fixed inset-0 bg-white z-[9999] pointer-events-none"
	style="transition: opacity {isFlashing ? '0ms' : '2500ms'} ease-out; opacity: {isFlashing ? '1' : '0'};"
></div>

{#if showInsult}
	<div class="fixed top-1/2 left-1/2 z-[10000] -translate-x-1/2 -translate-y-1/2 animate-in fade-in zoom-in-95 duration-500">
		<div class="bg-red-600 backdrop-blur-sm text-white font-black p-4 rounded-lg shadow-[0_0_50px_rgba(220,38,38,0.8)] max-w-sm border-4 border-white text-center transform rotate-[-2deg]">
			
			<h4 class="text-3xl uppercase mb-3 drop-shadow-md">NAH MAN 💀</h4>
			
			<div class="relative overflow-hidden rounded border-2 border-black mb-3">
				<img 
					src={catLaugh} 
					alt="Laughing Mockery" 
					class="w-full object-cover animate-pulse"
				/>
			</div>

			<div class="space-y-1 font-mono text-lg font-extrabold uppercase leading-tight drop-shadow-sm">
				<p>LOOK AT YOU.</p>
				<p class="text-sm font-bold opacity-90 normal-case my-2">(You actually thought light mode was cool ?)</p>
			</div>

		</div>
	</div>
{/if}