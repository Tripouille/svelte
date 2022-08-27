<style>
  .backdrop {
    position: fixed;
    inset: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.6);
  }

  .modal {
    padding: 10px;
    border-radius: 10px;
    margin: 10%;
    text-align: center;
    background-color: white;
    font-weight: bold;
    font-size: x-large;
  }

  .promo {
    background-color: crimson;
    color: white;
  }
</style>

<script>
  export let showModal = false;
  export let isPromo = false;
</script>

{#if showModal}
  <div class="backdrop" on:click|self>
    <div class="modal" class:promo={isPromo}>
      <slot />
    </div>
  </div>
{/if}
