<script>
  import '../app.postcss';
</script>

<svelte:head>
  <title>MiduTranslate</title>
  <link rel="icon" href="/favicon.ico" type="image/x-icon" />
  <meta name="theme-color" content="#0099ff" />
</svelte:head>

<div
  class="max-w-3xl p-6 mx-auto max-h-screen min-h-[500px] h-screen flex justify-center items-center flex-col relative text-white"
>
  <div class="w-full">
    <h1
      class="font-semibold text-5xl text-center mb-7 drop-shadow-[0_3px_5px_rgba(29,86,130,0.7)] -mt-20"
    >
      Traductor
    </h1>

    <div class="flex gap-x-3 mb-3">
      <slot />
    </div>

    <div class="flex items-center gap-3">
      <hr class="w-full border-b-px border-[#3c4654]" />
      <span class=" whitespace-nowrap font-light text-sm text-white/50">
        Por SoyLuisArrieta & <a
          class="text-[#199afc]"
          href="https://midu.dev/"
          target="_blank"
          rel="noopener noreferrer">Midudev</a
        >
      </span>
    </div>
  </div>

  <footer class="absolute bottom-4 flex justify-center h-16 gap-x-4">
    <img
      class="h-full grayscale scale-50"
      src="/javascript.png"
      alt="Logo Javascript"
    />
    <img class="h-full grayscale scale-50" src="/css.png" alt="Logo CSS" />
    <a
      class="inline-block hover:scale-105 transition-transform ease-in-out"
      href="https://midu.dev/"
      target="_blank"
      rel="noopener noreferrer"
    >
      <img class="w-auto h-full" src="/logo.png" alt="Logo Midudev" />
    </a>
    <img
      class="h-full grayscale scale-50"
      src="/svelte.png"
      alt="Logo Svelte"
    />
    <img
      class="h-full grayscale scale-50"
      src="/tailwind.png"
      alt="Logo Tailwind"
    />
  </footer>
</div>
