<script>
  import { expoInOut } from "svelte/easing";
  import { tweened } from "svelte/motion";
  import { onDestroy, onMount } from "svelte";
  import { globalHistory } from "svelte-navigator";
  import Icon from "@iconify/svelte";

  let pathname = window.location.pathname;

  const scrollToTop = () => {
    window.scrollTo({
      top: 0,
    });
  };

  const nav = tweened(100, {
    duration: 1000,
    easing: expoInOut,
  });

  setTimeout(() => {
    $nav -= 100;
  }, 200);

  let unsub;

  onMount(() => {
    unsub = globalHistory.listen(({ location, action }) => {
      pathname = location.pathname;
      setNavOpen(false);
    });
  });

  onDestroy(() => {
    unsub();
  });

  let navOpen = false;

  const setNavOpen = (state) => {
    navOpen = state;
  };
</script>

<header class="w-full z-[9999] absolute">
  <nav
    class="fixed left-0 top-0 z-[9999] w-full bg-neutral-900 py-8 px-9 flex justify-between"
    style="opacity: {(100 - $nav) / 100}"
  >
    <h1
      class="text-xl tracking-[0.325em] relative z-[9999] {navOpen
        ? 'text-neutral-900'
        : 'text-white'} transition-all delay-500 duration-700 font-medium"
      on:click={scrollToTop}
    >
      <span
        class="{navOpen
          ? 'text-amber-600'
          : 'text-amber-400'} font-bold transition-all delay-500 duration-700"
        >C</span
      >ODE<span
        class="{navOpen
          ? 'text-amber-600'
          : 'text-amber-400'} font-bold transition-all delay-500 duration-700"
        >B</span
      >LOG<br />
      <span class="text-xs tracking-widest block">by Melvin Chia.</span>
    </h1>
    <div class="hidden md:flex items-center gap-12 text-sm">
      {#each ["home", "work", "about", "blog"] as link}
        <div
          class="tracking-[0.325rem] relative uppercase after:transition-all after:duration-300 after:content-[''] after:w-0 after:absolute after:left-1/2 after:-translate-x-[56%] after:-bottom-1 after:border-b-[1.6px] after:border-amber-400 {pathname ===
            '/' + link ||
          (pathname === '/' && link === 'home')
            ? 'after:w-1/2'
            : ''} hover:after:w-1/2"
        >
          {link}
        </div>
      {/each}
    </div>
    <button
      on:click={() => setNavOpen(!navOpen)}
      class="block md:!hidden relative z-[9999]"
      aria-label="Toggle navigation"
    >
      <Icon
        icon="heroicons-outline:menu-alt-4"
        class="w-7 h-7 {navOpen ? 'text-neutral-900' : 'text-white'}"
      />
    </button>
    <div
      class="w-full h-screen bg-amber-400 {navOpen
        ? 'top-0 left-0 rounded-br-none'
        : '-top-full -left-full rounded-br-full'} transition-all duration-700 fixed pointer-events-none z-50 flex items-center justify-center text-neutral-900 font-semibold"
    >
      <div class="flex flex-col items-center gap-12 text-sm">
        {#each ["home", "work", "about", "blog"] as link}
          <div
            class="tracking-[0.325rem] relative uppercase {pathname ===
              '/' + link ||
            (pathname === '/' && link === 'home')
              ? "after:content-[''] after:absolute after:left-1/2 after:-translate-x-[56%] after:-bottom-1 after:w-1/2 after:border-b-2 after:border-neutral-900"
              : ''}"
          >
            {link}
          </div>
        {/each}
      </div>
    </div>
    <div
      class="fixed pointer-events-none bottom-8 items-center left-8 text-sm gap-8 -rotate-90 origin-top-left hidden md:flex"
    >
      <a
        href="//github.com/melvinchia3636"
        target="_blank"
        class="font-bold hover:text-amber-400 transition-all duration-500">gh</a
      >
      <a
        href="//facebook.com/TheSillyCoder"
        target="_blank"
        class="font-bold hover:text-amber-400 transition-all duration-500">fb</a
      >
      <a
        href="//www.youtube.com/channel/UCsSf5dUsiQYfEucaJlusXng"
        target="_blank"
        class="font-bold hover:text-amber-400 transition-all duration-500">yt</a
      >
      <div class="w-16 border-t-2 ml-1 border-neutral-600 hidden md:block" />
    </div>
    <div
      class="fixed pointer-events-none bottom-10 items-center right-10 text-sm hidden md:block"
    >
      v9.0.0
    </div>
  </nav>
</header>
