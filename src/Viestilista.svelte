<script>
  import viestit from './viestiStore';
  import { scale } from 'svelte/transition';
</script>

<main>
  {#each $viestit as v, i}
    <div transition:scale>
      <p>{i + 1}. viesti: {v.sanoma}</p>
    </div>
  {/each}
</main>
