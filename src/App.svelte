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
  <h1>Chuck on mies</h1>

  <!-- Alla oleva if-lause määrittelee apista otetun tiedon näkyvyyden.
  Info komponentissa oleva  timeout funktio sulkee ikkunan tietyn ajan kuluttua.-->

  {#if infoVisible}
    <Info on:hideinfo={() => (infoVisible = false)} />
  {/if}

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
  <p>Paina saadaksesi Chuck Norrisista faktan</p>

  <!-- Napilla infoikkuna aukeaa -->

  <Button
    on:click={() => {
      infoVisible = true;
    }}>Jee</Button
  >
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

  <Viestilista />
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
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
  article {
    padding: 1em;
  }
  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
