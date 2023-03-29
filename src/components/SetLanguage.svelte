<script>
  export let value = 'es';

  import { SUPPORTED_LANGUAGES } from '../contants';
</script>

<select
  class="w-full bg-transparent p-2 border border-[#3c4654] rounded focus-visible:outline-none focus:border-[#199afc] text-[#96c8ee] text-opacity-80"
  bind:value
>
  {#each SUPPORTED_LANGUAGES as { code, label }}
    <option class="bg-[#20252C] text-white border-[#199afc]" value={code}>
      {label}
    </option>
  {/each}
</select>
