<style>
  main {
    max-width: 600px;
    margin: 3rem auto;
  }
</style>

<script>
  import Footer from "./components/Footer.svelte";
  import Header from "./components/Header.svelte";
  import Tabs from "./shared/Tabs.svelte";

  let items = ["Current Polls", "Add New Poll"];
  let activeItem = items[0];
  function changeActiveItem({ detail: item }) {
    activeItem = item;
  }
</script>

<Header />
<main>
  <Tabs {items} {activeItem} on:itemClick={changeActiveItem} />
  {#if activeItem === "Current Polls"}
    <p>Current Polls</p>
  {:else if activeItem === "Add New Poll"}
    <p>Add New Poll</p>
  {/if}
</main>
<Footer />
