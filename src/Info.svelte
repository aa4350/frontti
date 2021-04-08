<script>
  import { fly, blur, fade } from 'svelte/transition';
  import { elasticOut } from 'svelte/easing';
  import { createEventDispatcher, onMount } from 'svelte';

  const dispatch = createEventDispatcher();

  setTimeout(() => {
    dispatch('hideinfo');
  }, 7000);
  let joke = '';

  const fetchJoke = async () => {
    const response = await fetch('https://api.chucknorris.io/jokes/random');
    const data = await response.json();
    joke = data.value;
  };

  onMount(fetchJoke);
</script>

<div
  class="info"
  in:fly={{ duration: 1500, x: 0, y: -200, easing: elasticOut }}
  out:blur
  on:click={fetchJoke}
>
  <div>
    <p><span transition:fade={{ duration: 1000 }}>{joke}</span></p>
  </div>
</div>

<style>
  .info {
    position: fixed;
    top: 30%;
    left: 2em;
    width: 20em;
    height: 9em;
    background-color: #ccc;
    box-shadow: 0 3px 8px rgba(0, 0, 0, 0.3);
    text-align: center;
    padding: 1em;
  }
  span {
    vertical-align: middle;
  }
</style>
