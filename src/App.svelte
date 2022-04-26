<script>
  import { tweened } from "svelte/motion";
  import { expoInOut } from "svelte/easing";
  import { fade } from "svelte/transition";
  import TypedJs from "@loscrackitos/svelte-typed-js";
import Navbar from "./Navbar.svelte";

  const size = tweened(0, {
    duration: 1500,
    easing: expoInOut,
  });

  const size2 = tweened(50, {
    duration: 1500,
    easing: expoInOut,
  });

  let bind = false;
  let bind2 = false;

  setTimeout(() => {
    bind = true;
  }, 500);

  setTimeout(() => {
    $size += 400;
  }, 1000);

  setTimeout(() => {
    $size2 += 20;
  }, 1500);

  setTimeout(() => {
    bind2 = true;
  }, 2000);
</script>

<div class="w-full bg-neutral-900 text-neutral-200 h-screen flex items-center justify-center">
  <Navbar />
  <div
    class="flex flex-col items-center"
    style="max-height: {$size2}px"
  >
    {#if bind}
      <div
        class="text-4xl sm:text-9xl fixed pointer-events-none top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 opacity-[2%] tracking-[0.325em] -mt-3 font-black"
        in:fade
        out:fade
      >
        &lt;CODEBLOG/&gt;
      </div>
      <div
        class="text-3xl sm:text-5xl tracking-[0.325em] flex"
        in:fade={{ delay: 250, duration: 300 }}
        out:fade={{ delay: 250, duration: 300 }}
      >
        <div>&lt;</div>
        <div
          class="overflow-hidden flex justify-center items-center"
          style="max-width: {$size}px"
        >
          CODEBLOG
        </div>
        <div>/&gt;</div>
      </div>
    {/if}
    {#if bind2}
      <div
        class="tracking-[0.325em] type flex font-light text-amber-400 -ml-1 text-sm sm:text-base px-8 text-center mt-4"
        in:fade={{ duration: 300 }}
      >
        <TypedJs
          strings={[
            "COMING SOON",
          ]}
          showCursor={false}
          typeSpeed={100}
          backSpeed={50}
          backDelay={1500}
        >
          /*
          <h1 class="typing" />
          */
        </TypedJs>
      </div>
    {/if}
  </div>
</div>

<style global>
  .type > div {
    display: flex;
  }
</style>
