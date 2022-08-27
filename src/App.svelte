<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }
</style>

<script>
  import AddPersonForm from "./AddPersonForm.svelte";
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

  function addPerson(event) {
    console.log(event);
    people = [event.detail, ...people];
    toggleModal();
  }
</script>

<main>
  <Modal {showModal} isPromo on:click={toggleModal}>
    <h3>Add a New Person</h3>
    <AddPersonForm on:addPerson={addPerson} />
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
