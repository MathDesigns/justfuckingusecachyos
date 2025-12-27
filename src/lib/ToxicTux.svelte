<script lang="ts">
	import { onMount } from 'svelte';
    import unhingedTux from '$lib/assets/unhinged_tux.png';

	// Svelte 5 Runes
	let isVisible = $state(false);
	let message = $state("");
	let position = $state({ top: 110, left: 110 }); 
	let dodgeCount = $state(0);
	let isDead = $state(false);

	const quotes = [
		"I see you scrolling. Have you run 'pacman -Syu' today or are you looking for a participation trophy?",
		"Nice GPU. Shame your drivers are proprietary garbage.",
		"Are you going to download the ISO or just stare at it? My compile time is worth more than your life.",
		"I bet you use 'nano' because you don't know how to exit 'vim'. Pathetic.",
		"Is that a mouse? Real users use keyboard shortcuts. Touch grass.",
		"Your cursor movement is sluggish. Just like your kernel header compilation.",
		"Do not touch me. I am compiled from source. You are a binary blob."
	];

	onMount(() => {
		const interval = setInterval(() => {
			if (!isVisible && !isDead && Math.random() > 0.3) {
				spawnTux();
			}
		}, 8000); 

		setTimeout(spawnTux, 2500);

		return () => clearInterval(interval);
	});

	function spawnTux() {
		message = quotes[Math.floor(Math.random() * quotes.length)];
		isVisible = true;
		dodgeCount = 0;
		const side = Math.random() > 0.5 ? 'left' : 'right';
		
		position = { 
			top: Math.floor(Math.random() * 30) + 50,
			left: side === 'left' ? Math.floor(Math.random() * 20) + 5 : Math.floor(Math.random() * 20) + 60
		};
	}

	function tryToClose() {
		if (dodgeCount < 5) {
			position = {
				top: Math.floor(Math.random() * 70) + 10,
				left: Math.floor(Math.random() * 70) + 10
			};
			dodgeCount++;
			
			if (dodgeCount === 1) message = "Too slow. Upgrade your reaction time.";
			if (dodgeCount === 2) message = "You can't catch root privileges, and you can't catch me.";
			if (dodgeCount === 3) message = "Stop clicking. Start compiling.";
            if (dodgeCount === 4) message = "I CAN DO THIS ALL DAY.";
		} else {
			killTux();
		}
	}

	function killTux() {
		isDead = true;
		message = "SEGMENTATION FAULT. CORE DUMPED.";
		setTimeout(() => {
			isVisible = false;
			isDead = false;
		}, 2500);
	}
</script>

{#if isVisible}
	<div 
		class="hidden md:block fixed z-[60] w-64 md:w-80 transition-all duration-150 ease-out cursor-crosshair {isDead ? 'animate-ping opacity-0' : ''}"
		style="top: {position.top}%; left: {position.left}%;"
	>
		
		<div class="relative bg-yellow-400 border-[5px] border-black p-4 mb-6 shadow-[12px_12px_0px_0px_rgba(0,0,0,1)] animate-in slide-in-from-bottom-5 duration-300">
			<div class="absolute -bottom-8 left-1/2 -translate-x-1/2 w-0 h-0 border-l-[20px] border-l-transparent border-r-[20px] border-r-transparent border-t-[30px] border-t-black"></div>
			<div class="absolute -bottom-[22px] left-1/2 -translate-x-1/2 w-0 h-0 border-l-[12px] border-l-transparent border-r-[12px] border-r-transparent border-t-[22px] border-t-yellow-400"></div>
			
			<p class="font-mono text-lg font-black text-black leading-[1.1] uppercase tracking-tight">
				{message}
			</p>

			<button 
				onmouseenter={tryToClose} 
				class="absolute -top-6 -right-6 bg-red-600 text-white w-10 h-10 flex items-center justify-center border-[5px] border-black text-lg font-black hover:bg-red-500 shadow-[6px_6px_0px_0px_rgba(0,0,0,1)]"
			>
				X
			</button>
		</div>

		<div class="relative group">
            <img 
                src={unhingedTux} 
                alt="Toxic Tux" 
                class="w-full h-auto relative z-10 drop-shadow-[0_0_30px_rgba(50,255,50,0.8)] tux-glitch"
            />
		</div>

	</div>
{/if}

<style>
    @keyframes glitch-anim {
        0% { transform: translate(0) skew(0deg); filter: hue-rotate(0deg); }
        20% { transform: translate(-3px, 2px) skew(2deg); filter: hue-rotate(15deg); }
        40% { transform: translate(-3px, -2px) skew(-2deg); }
        60% { transform: translate(3px, 2px) skew(1deg); filter: hue-rotate(-15deg); }
        80% { transform: translate(3px, -2px) skew(-1deg); }
        100% { transform: translate(0) skew(0deg); filter: hue-rotate(0deg); }
    }

    .tux-glitch {
        animation: glitch-anim 0.5s infinite linear alternate-reverse;
        filter: drop-shadow(0 0 30px rgba(50, 255, 50, 0.8));
    }
</style>