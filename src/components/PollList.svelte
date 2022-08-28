<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 1rem;
    list-style: none;
  }
</style>

<script>
  import PollDetails from "./PollDetails.svelte";

  export let polls;
</script>

<ul class="poll-list">
  {#each polls as poll}
    <li class="poll-item">
      <PollDetails {poll} on:vote />
    </li>
  {/each}
</ul>
