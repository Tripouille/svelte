<style>
</style>

<script>
  import { createEventDispatcher } from "svelte";
  export let poll;

  const dispatch = createEventDispatcher();
  function handleVote(answer) {
    dispatch("vote", { poll, answer });
  }
  $: total = poll.votesA + poll.votesB;
</script>

<p style="font-weight: bold">{poll.question} ({total})</p>
<p style="cursor: pointer" on:click={() => handleVote("votesA")}>
  {poll.answerA}
  ({poll.votesA})
</p>
<p style="cursor: pointer" on:click={() => handleVote("votesB")}>
  {poll.answerB}
  ({poll.votesB})
</p>
