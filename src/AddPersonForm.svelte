<style>
  form {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    row-gap: 1rem;
    border: 2px solid white;
    padding: 1rem;
    border-radius: 1rem;
  }
</style>

<script>
  import { v4 as uuid } from "uuid";
  import { createEventDispatcher } from "svelte";
  let dispatch = createEventDispatcher();

  let name;
  let beltColour;
  let age = 18;
  let skills = [];

  function handleSubmit() {
    const person = { name, beltColour, age, id: uuid() };
    dispatch("addPerson", person);
  }
</script>

<form on:submit|preventDefault={handleSubmit}>
  <input type="text" placeholder="name" id="name" bind:value={name} />
  <label>
    <span>Belt Color</span>
    <select bind:value={beltColour}>
      <option value="black">black</option>
      <option value="red">red</option>
      <option value="green">green</option>
      <option value="blue">blue</option>
    </select>
  </label>
  <input type="number" id="age" min={10} max={99} step={1} bind:value={age} />
  <fieldset>
    <legend>Skills</legend>
    <label>
      <span>fighting</span>
      <input type="checkbox" value="fighting" bind:group={skills} />
    </label>
    <label>
      <span>running</span>
      <input type="checkbox" value="running" bind:group={skills} />
    </label>
  </fieldset>
  <button type="submit">Add Person</button>
</form>
