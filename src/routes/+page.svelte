<script lang="ts">
  import ComparisonTable from "$lib/ComparisonTable.svelte";
  import Flashbang from "$lib/Flashbang.svelte";
  import ToxicTux from "$lib/ToxicTux.svelte";

  let angerLevel: number = $state(0);
  let timeSaved = $derived(angerLevel * 4.5);

  const excuses: string[] = [
    "But I like configuring GRUB manually...",
    "Ubuntu is user friendly though...",
    "I haven't compiled my kernel today...",
    "What about stability?",
    "I use Arch BTW (the slow way)",
  ];

  let currentExcuse: number = $state(0);

  const increaseAnger = (): void => {
    angerLevel += 1;
  };

  function nextExcuse(): void {
    currentExcuse = (currentExcuse + 1) % excuses.length;
    increaseAnger();
  }
</script>

<svelte:head>
  <title>Just Fucking Use CachyOS</title>
</svelte:head>

<Flashbang />
<ToxicTux />

<main class="flex w-full flex-col items-center overflow-x-hidden">
  <header
    class="max-w-3xl space-y-6 px-6 py-20 text-center md:py-32 md:text-left"
  >
    <h1
      class="text-6xl font-black leading-[0.9] tracking-tighter text-white md:text-8xl"
    >
      JUST FUCKING USE <br />
      <span class="text-emerald-400 decoration-wavy decoration-4 underline"
        >CACHYOS</span
      >.
    </h1>
    <p class="max-w-2xl text-xl font-bold text-gray-400 md:text-2xl">
      You are wasting your life waiting for packages to compile. Stop it.
    </p>
  </header>

  <section class="mb-12 w-full max-w-3xl px-6">
    <div class="space-y-4 border-l-4 border-red-500 py-2 pl-6">
      <h2 class="text-3xl font-bold uppercase tracking-widest text-red-500">
        The Issue With You
      </h2>
      <p class="text-lg text-gray-300">
        You think you're cool because you installed Arch manually?
        Congratulations, you know how to read a Wiki. Meanwhile, your CPU is
        sleeping because you're using generic binaries compiled for a toaster
        from 2008.
      </p>
      <p class="text-lg text-gray-300">
        <strong class="text-white">CachyOS</strong> is Arch, but for people who actually
        have shit to do.
      </p>
    </div>
  </section>

  <ComparisonTable />

  <section class="my-20 w-full max-w-3xl px-6">
    <div
      class="rounded-none border-2 border-emerald-500/20 bg-[#1a1a1a] p-8 shadow-[8px_8px_0px_0px_rgba(16,185,129,1)]"
    >
      <div
        class="flex flex-col items-start justify-between gap-6 md:flex-row md:items-center"
      >
        <div>
          <h3 class="mb-2 text-xl font-bold text-white">
            Try to make an excuse:
          </h3>
          <button
            onclick={nextExcuse}
            class="cursor-pointer border border-gray-600 bg-gray-800 px-6 py-3 font-bold uppercase text-white transition-transform hover:bg-gray-700 active:scale-95"
            type="button"
          >
            "{excuses[currentExcuse]}"
          </button>
        </div>
        <div class="text-right">
          <div
            class="text-sm font-bold uppercase tracking-widest text-gray-500"
          >
            Time wasted not using Cachy
          </div>
          <div
            class="font-mono text-5xl font-black tabular-nums text-emerald-400"
          >
            {timeSaved.toFixed(1)}s
          </div>
          {#if angerLevel > 5}
            <div class="animate-pulse mt-2 text-xs font-bold text-red-500">
              NOBODY CARES ABOUT YOUR CONFIG
            </div>
          {/if}
        </div>
      </div>
    </div>
  </section>

  <section class="mb-20 w-full max-w-3xl space-y-12 px-6">
    <article>
      <h3 class="mb-4 text-4xl font-black text-white">
        x86-64-v3 Optimized Binaries
      </h3>
      <p class="text-lg leading-relaxed text-gray-400">
        You don’t even know what AVX2 or AVX-512 does, do you? You just complain
        your rig feels sluggish.<br />
        CachyOS recompiles everything to actually use the CPU you paid premium for
        instead of babysitting 20-year-old fossils.<br />
        If your processor predates smartphones, get the fuck off this page.
      </p>
    </article>

    <article>
      <h3 class="mb-4 text-4xl font-black text-white">The BORE Scheduler</h3>
      <p class="text-lg leading-relaxed text-gray-400">
        It stands for <span class="font-bold text-emerald-400"
          >Burst-Oriented Response Enhancer</span
        >. It prioritizes the window you are actually looking at. Unlike the
        stock scheduler, which prioritizes some background systemd process that
        does literally nothing. Your mouse feels smoother. Your games stutter
        less. It's not magic, it's just better code.
      </p>
    </article>

    <article>
      <h3 class="mb-4 text-4xl font-black text-white">The GUI Installer</h3>
      <p class="text-lg leading-relaxed text-gray-400">
        "But real men use the CLI!"
        <br /><br />
        Shut the fuck up.
        <br /><br />
        It installs a fully optimized Arch system in 5 minutes with ZFS, Btrfs, or
        whatever weird file system you claim to need. Then it installs the NVIDIA
        drivers correctly. automatically. Go ahead, try to install NVIDIA drivers
        manually on a hybrid laptop. See you in 3 days.
      </p>
    </article>
  </section>

  <footer class="w-full pb-10 pt-20">
    <div
      class="mx-auto flex max-w-3xl flex-col items-center space-y-8 px-6 text-center"
    >
      <h2 class="text-5xl font-black text-white md:text-7xl">DO IT.</h2>
      <a
        href="https://cachyos.org/download"
        target="_blank"
        rel="noopener noreferrer"
        class="inline-block transform bg-emerald-500 px-12 py-6 text-2xl font-black text-black shadow-[0px_0px_40px_rgba(16,185,129,0.6)] transition-all hover:-translate-y-2 hover:bg-emerald-400 md:text-4xl"
      >
        DOWNLOAD ISO
      </a>
      <p class="max-w-md text-sm text-gray-400">
        By clicking this you admit that you want a faster computer and are tired
        of pretending generic binaries are "good enough."
      </p>

      <div class="mt-12 text-center font-mono text-xs text-gray-400">
        <p class="mb-4">
          Built with Svelte 5 (Runes) & Tailwind v4 because we like bleeding
          edge, just like your OS should be.
        </p>
        <p>
          Inspired by
          <a
            href="https://motherfuckingwebsite.com/"
            target="_blank"
            rel="noreferrer"
            class="underline hover:text-gray-400">motherfuckingwebsite.com</a
          >,
          <a
            href="https://justfuckingusetailwind.com/"
            target="_blank"
            rel="noreferrer"
            class="underline hover:text-gray-400">justfuckingusetailwind.com</a
          >,
          <a
            href="https://justfuckingusereact.com/"
            target="_blank"
            rel="noreferrer"
            class="underline hover:text-gray-400">justfuckingusereact.com</a
          >, and
          <a
            href="https://justfuckingusehtml.com/"
            target="_blank"
            rel="noreferrer"
            class="underline hover:text-gray-400">justfuckingusehtml.com</a
          >.
        </p>
      </div>
    </div>
  </footer>
</main>
