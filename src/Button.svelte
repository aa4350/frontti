<button on:click><slot>Tyhjennä</slot></button>

<style>
  button {
    display: inline-block;
    padding: 0.35em 1.2em;
    border: 0.1em solid #ffffff;
    margin: 0 0.3em 0.3em 0;
    border-radius: 0.12em;
    box-sizing: border-box;
    text-decoration: none;
    font-family: 'Roboto', sans-serif;
    font-weight: 300;
    color: #ff7e29;
    text-align: center;
    transition: all 0.2s;
    box-shadow: 1px 1px black;
  }
  button:hover {
    color: #000000;
    background-color: #bbbbbb;
  }
</style>
