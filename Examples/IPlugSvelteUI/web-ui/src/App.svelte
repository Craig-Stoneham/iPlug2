<script lang="ts">
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from './assets/vite.svg'
  import iPlugLogo from './assets/iplug.png'
  import Knob from './lib/Knob.svelte'

  let knobComponent: any;

  // Handle parameter value changes from the plugin
  window.SPVFD = (paramIdx: number, val: number) => {
    // If this is the parameter for our knob, update it
    if (paramIdx === 0) { // Assuming paramId=1 for the volume knob
      const actualValue = 0 + (val * (100 - 0)); // Convert normalized value using min/max
      knobComponent?.setValueFromPlugin(actualValue);
    }
  };
</script>

<main>
  <div>
    <a href="https://vite.dev" target="_blank" rel="noreferrer">
      <img src={viteLogo} class="logo" alt="Vite Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank" rel="noreferrer">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
    <a href="https://iplug2.github.io" target="_blank" rel="noreferrer">
      <img src={iPlugLogo} class="logo iplug" alt="iPlug Logo" />
    </a>
  </div>
  <h1>Vite + Svelte + iPlug2</h1>

  <Knob 
    bind:this={knobComponent}
    paramId={0}
    label="Volume"
    minValue={0}
    maxValue={100}
    units="dB"
    defaultValue={50}
  />
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  :global(*) {
    user-select: none;
    -webkit-user-select: none; /* Safari */
    -moz-user-select: none; /* Firefox */
    -ms-user-select: none; /* IE10+/Edge */
  }
</style>
