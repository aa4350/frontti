<script>
  import viestit from './viestiStore';
  import { scale } from 'svelte/transition';
</script>

<!-- Each lohko joka ottaa kaikki viestit storesta ja listaa ne. -->

<main>
  {#each $viestit as v, i}
    <div transition:scale>
      <p>{i + 1}. viesti: {v.sanoma}</p>
    </div>
  {/each}
</main>
