<style>
  button {
    border-radius: 0.5rem;
    cursor: pointer;
    padding: 0.5rem 1rem;
    font-weight: bold;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
  }

  .primary {
    background-color: purple;
    color: white;
  }

  .secondary {
    background-color: aquamarine;
    color: white;
  }

  .flat {
    box-shadow: none;
  }

  .inverse {
    mix-blend-mode: difference;
  }
</style>

<script>
  export let type = "primary";
  export let flat = false;
  export let inverse = false;
  export let props;
</script>

<button class={type} class:flat class:inverse {...props}><slot /></button>
