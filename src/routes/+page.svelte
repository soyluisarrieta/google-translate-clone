<script>
  import SetLanguage from '../components/SetLanguage.svelte';

  let SET_FROM_LANGUAGE = 'es';
  let SET_TO_LANGUAGE = 'en';
  let SET_FROM_TEXT = '';
  let SET_TO_TEXT = '';
  let TRANSLATION = '';

  $: {
    if (SET_FROM_LANGUAGE.length && SET_TO_LANGUAGE.length) {
      console.log(SET_FROM_LANGUAGE, SET_TO_LANGUAGE);
    }
  }

  const handleToTranslate = () => {};
</script>

<div class="w-full p-1">
  <SetLanguage bind:value={SET_FROM_LANGUAGE} />

  <textarea
    class="w-full h-40 text-3xl p-4 bg-transparent mt-3 focus-visible:outline-none"
    placeholder="Ingresar texto"
    on:input={handleToTranslate}
  />
</div>

<div class="w-auto h-12 flex justify-center p-2">
  <svg
    class="h-full fill-white/20 hover:fill-white/50 cursor-pointer"
    focusable="false"
    xmlns="http://www.w3.org/2000/svg"
    viewBox="0 0 24 24"
    ><path
      d="M6.99 11L3 15l3.99 4v-3H14v-2H6.99v-3zM21 9l-3.99-4v3H10v2h7.01v3L21 9z"
    /></svg
  >
</div>

<div class="w-full p-1 flex flex-col">
  <SetLanguage bind:value={SET_TO_LANGUAGE} />
  <div class="w-full h-full bg-white/5 rounded mt-3">
    <p class="w-full h-full text-3xl p-4" class:opacity-30={!TRANSLATION}>
      {@html TRANSLATION || 'Traducción'}
    </p>
  </div>
</div>
