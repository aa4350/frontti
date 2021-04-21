<script>
  import Button from './Button.svelte';
  import Info from './Info.svelte';
  import Modal from './Modal.svelte';
  import Viestilista from './Viestilista.svelte';
  import viestit from './viestiStore';

  let modal = false;
  let infoVisible = false;
  let nimi;
  let osoite;
  let viesti;

  //Tämä on funktio joka suoritetaan kun painetaan nappia modalissa tai backdroppia
  //Kentät tyhjentyy, modal häviää ja viestit store päivittyy viestikentän sisällöllä

  const sulje = () => {
    modal = false;
    nimi = '';
    osoite = '';
    viestit.update((i) => [...i, { sanoma: viesti }]);
    viesti = '';
  };
</script>

<main>
  <div class="otsikko">
    <h1><b>Chuck</b> on mies</h1>
  </div>
  <!-- Alla oleva if-lause määrittelee apista otetun tiedon näkyvyyden.
  Info komponentissa oleva  timeout funktio sulkee ikkunan tietyn ajan kuluttua.-->

  {#if infoVisible}
    <Info on:hideinfo={() => (infoVisible = false)} />
  {/if}

  <hr />

  <!-- Modalin koodia. Välitetään on:click tapahtuma, jossa funktiona sulje funktio. -->

  {#if modal}
    <Modal on:click={sulje}
      ><h2>Viestin loppukatsaus</h2>
      <hr />
      <p>Nimi: {nimi}</p>
      <p>Osoite: {osoite}</p>
      <p>Viesti: {viesti}</p></Modal
    >
  {/if}
  <div class="fact">
    <p>Paina saadaksesi Chuck Norrisista faktan</p>

    <!-- Napilla infoikkuna aukeaa -->

    <Button
      on:click={() => {
        infoVisible = true;
      }}>Jee</Button
    >
  </div>
  <hr />
  <article>
    <h3>Lähetä Chuckille persoonallinen viesti:</h3>

    <!-- Form elementit alla, arvot bindattu muuttujiin -->

    <div>
      <div>
        <input type="text" placeholder="Nimi" id="nimi" bind:value={nimi} />
      </div>
      <div>
        <input
          type="text"
          placeholder="Kotiosoite (Chuckille tiedoksi)"
          id="osot"
          bind:value={osoite}
        />
      </div>
      <div>
        <textarea
          name="viesti"
          id="viesti"
          cols="50"
          rows="7"
          placeholder="Viestisi"
          bind:value={viesti}
        />
      </div>
    </div>

    <!-- Napin painalluksella modal ikkuna ilmestyy. -->

    <Button on:click={() => (modal = true)}>Tulosta ja lähetä</Button>
  </article>
  <hr />
  <h3>Lähetetyt viestit</h3>

  <!-- Each lohkon sisältävä listakomponentti -->
  {#if $viestit.length > 0}
    <Viestilista />
  {:else}
    <p>Ei vielä viestejä</p>
  {/if}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
    background-color: rgb(247, 240, 255);
    height: 100%;
  }

  h1 {
    margin: auto;
    color: #200065;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
    background-color: rgb(244, 234, 255);
    width: 40%;
    box-shadow: 1px 1px black;
  }
  div {
    padding: 0.5em;
  }
  #nimi {
    width: auto;
  }
  #osot {
    width: 20em;
  }
  article,
  .fact,
  .otsikko {
    padding: 1em;
  }
  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
