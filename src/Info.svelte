<script>
  import { fly, blur, fade } from 'svelte/transition';
  import { elasticOut } from 'svelte/easing';
  import { createEventDispatcher, onMount } from 'svelte';

  const dispatch = createEventDispatcher();

  //Tältä alueelta löytyy custom eventin asiat sekä infoikkunan sulkemiseen käytettävä timeout

  setTimeout(() => {
    dispatch('hideinfo');
  }, 7000);
  let joke = '';

  //Ulkopuolisen tietokannan dataa kutsutaan ja data merkataan joke muuttajalle.

  const fetchJoke = async () => {
    const response = await fetch('https://api.chucknorris.io/jokes/random');
    const data = await response.json();
    joke = data.value;
  };

  //onMount sisältö toteutuu kun komponentin sisältö on renderöity

  onMount(fetchJoke);
</script>

<!-- transitioita -->

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
