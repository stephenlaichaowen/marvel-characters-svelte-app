<script>
  let idx = 0;
  let len = 3;
  let isAscending = false;
  import Card from "./Card.svelte";
  import Button from "./Button.svelte";
  import { flip } from "svelte/animate";
  let arr;
  $: {
    arr = [...Array(len).keys()].map(x => idx + x);
    if (isAscending) arr.reverse();
  }
</script>

<main class="App">
  <h1>
    Characters of
    <em>Stan Lee</em>
  </h1>
  <div class="controls">
      <label>
        Show
        <input type="number" bind:value={len} min="0" />
      </label>
      <div>
        <input id="ascending" type="checkbox" bind:checked={isAscending} />
        <label for="ascending">Ascending?</label>
      </div>
    <Button on:click={() => idx++}>{idx}</Button>
  </div>
  <div class="wrap">
    {#each arr as id (id)}
      <div animate:flip={{ duration: 500 }}>
        <Card idx={id} />
      </div>
    {:else}
      <img
        alt="snap"
        src="https://i.insider.com/5ae3327e19ee8657008b45f6?width=750&format=jpeg&auto=webp"
      />
    {/each}
  </div>
</main>

<style>
  .controls {
    max-width: 1440px;
    margin: auto;
    display: flex;
  }
  .wrap {
    max-width: 1440px;
    margin: auto;
    /* border: 1px solid; */
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));    
  }
  @media (max-width: 560px) {
    .controls {
      flex-direction: column;
      /* align-items: flex-start; */
    }
  }
</style>
