<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }
</style>

<script>
  import Modal from "./Modal.svelte";

  let people = [
    { name: "yoshi", beltColour: "black", age: 25, id: 0 },
    { name: "mario", beltColour: "orange", age: 45, id: 1 },
    { name: "luigi", beltColour: "brown", age: 35, id: 2 },
  ];

  function deletePersonById(id) {
    return () => {
      people = people.filter((person) => person.id !== id);
    };
  }
  let num = 4;
  let showModal = false;
  let nameInput;
  function toggleModal() {
    showModal = !showModal;
  }

  function addNewPerson({ target }) {
    const { value: name } = target.name;
    const { value: beltColour } = target.beltColour;
    people = people.concat({ name, beltColour, age: 18, id: people.length });
    showModal = false;
  }
</script>

<main>
  <Modal {showModal} isPromo on:click={toggleModal}>
    <h3>Add a New Person</h3>
    <form on:submit|preventDefault={addNewPerson}>
      <input type="text" placeholder="name" id="name" />
      <input type="text" placeholder="belt colour" id="beltColour" />
      <button type="submit">Add Person</button>
    </form>
  </Modal>
  <button on:click={toggleModal}>Show New Person modal</button>
  {#each people as person (person.id)}
    <div>
      <h4>{person.name}</h4>
      {#if person.beltColour === "black"}
        <p><strong>Master Ninja</strong></p>
      {/if}
      <p class="badge" style="color: {person.beltColour}">
        {person.age} years old, {person.beltColour} belt.
      </p>
      <button on:click={deletePersonById(person.id)}>delete</button>
    </div>
  {:else}
    <p>No people found.</p>
  {/each}
</main>
