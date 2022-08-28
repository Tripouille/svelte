<style>
  main {
    max-width: 600px;
    margin: 3rem auto;
  }
</style>

<script>
  import CreatePollForm from "./components/CreatePollForm.svelte";
  import Footer from "./components/Footer.svelte";
  import Header from "./components/Header.svelte";
  import PollList from "./components/PollList.svelte";
  import Tabs from "./shared/Tabs.svelte";

  let items = ["Current Polls", "Add New Poll"];
  let activeItem = items[0];
  function changeActiveItem({ detail: item }) {
    activeItem = item;
  }

  let polls = [
    {
      question: "Do you like fish ?",
      answerA: "Yes",
      answerB: "No",
      votesA: 0,
      votesB: 0,
      id: "7f90dd69-9637-4aa0-bc7d-4d61af7acc48",
    },
  ];
  function handleSubmitPoll({ detail: poll }) {
    console.log("adding poll", poll);
    polls = [poll, ...polls];
    activeItem = items[0];
  }
  function handleVote({ detail: { poll, answer } }) {
    console.log("voting for", poll, answer);
    polls = polls.map((p) => {
      if (p.id === poll.id) {
        p[answer]++;
      }
      return p;
    });
  }
</script>

<Header />
<main>
  <Tabs {items} {activeItem} on:itemClick={changeActiveItem} />
  {#if activeItem === "Current Polls"}
    <PollList {polls} on:vote={handleVote} />
  {:else if activeItem === "Add New Poll"}
    <CreatePollForm on:submitPoll={handleSubmitPoll} />
  {/if}
</main>
<Footer />
