<script>
  import SetLanguage from '../components/SetLanguage.svelte';
  import {
    Configuration,
    OpenAIApi,
    ChatCompletionRequestMessageRoleEnum,
  } from 'openai';
  import { CONTEXT } from '../contants';

  let SET_FROM_LANGUAGE = 'es';
  let SET_TO_LANGUAGE = 'en';
  let SET_TO_TRANSLATE = '';
  let TRANSLATION = '';
  let LOADING = false;
  let debounceTimeoutId = 0;

  // OpenAI API
  const config = new Configuration({
    apiKey: import.meta.env.VITE_OPENAI_API_KEY,
  });

  const OpenAI = new OpenAIApi(config);

  // Func to translate
  const translate = () => {
    LOADING = true;
    clearTimeout(debounceTimeoutId);

    if (SET_TO_TRANSLATE.length) {
      debounceTimeoutId = setTimeout(async () => {
        Request;
        const response = await OpenAI.createChatCompletion({
          model: 'gpt-3.5-turbo',
          messages: [
            ...CONTEXT,
            {
              role: ChatCompletionRequestMessageRoleEnum.User,
              content: `${SET_TO_TRANSLATE} {{${SET_FROM_LANGUAGE}}} [[${SET_TO_LANGUAGE}]]`,
            },
          ],
          temperature: 0.7,
          max_tokens: 256,
        });

        TRANSLATION = response.data.choices[0].message?.content || '';
      }, 1500);
    } else {
      TRANSLATION = '';
    }

    LOADING = false;
  };

  // Observer
  $: SET_FROM_LANGUAGE && SET_TO_LANGUAGE && SET_TO_TRANSLATE && translate();

  // Exchange setters
  const exchangeSetters = () => {
    [SET_FROM_LANGUAGE, SET_TO_LANGUAGE] = [SET_TO_LANGUAGE, SET_FROM_LANGUAGE];
  };
</script>

<div class="w-full p-1">
  <SetLanguage bind:value={SET_FROM_LANGUAGE} />

  <textarea
    class="w-full h-40 text-3xl p-4 bg-transparent mt-3 focus-visible:outline-none"
    placeholder="Ingresar texto"
    bind:value={SET_TO_TRANSLATE}
    on:input={translate}
  />
</div>

<button class="w-7 h-7 flex justify-center mt-3" on:click={exchangeSetters}>
  <svg
    class="h-full fill-white/20 hover:fill-white/50 cursor-pointer"
    focusable="false"
    xmlns="http://www.w3.org/2000/svg"
    viewBox="0 0 24 24"
    ><path
      d="M6.99 11L3 15l3.99 4v-3H14v-2H6.99v-3zM21 9l-3.99-4v3H10v2h7.01v3L21 9z"
    /></svg
  >
</button>

<div class="w-full p-1 flex flex-col">
  <SetLanguage bind:value={SET_TO_LANGUAGE} />
  <div
    class="w-full h-full bg-white/5 rounded mt-3"
    class:animate-pulse={LOADING}
  >
    <div
      class="w-full h-full text-3xl p-4 relative justify-center items-center"
    >
      {#if LOADING}
        <p class="opacity-30 select-none pointer-events-none">Traduciendo...</p>
      {:else}
        <p class:opacity-30={!LOADING && !TRANSLATION}>
          {TRANSLATION || 'Traducción'}
        </p>
      {/if}
    </div>
  </div>
</div>
