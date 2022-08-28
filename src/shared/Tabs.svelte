<style>
  .tabs {
    margin-bottom: 3em;
  }

  .active {
    border-bottom: 2px solid red;
    color: red;
  }

  ul {
    display: flex;
    column-gap: 2em;
    list-style-type: none;
    justify-content: center;
  }

  li {
    padding-bottom: 0.5em;
    cursor: pointer;
  }
</style>

<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  export let items;
  export let activeItem;

  function onItemClick(item) {
    return () => dispatch("itemClick", item);
  }
</script>

<div class="tabs">
  <ul>
    {#each items as item}
      <li on:click={onItemClick(item)} class:active={activeItem === item}>
        <div>{item}</div>
      </li>
    {/each}
  </ul>
</div>
