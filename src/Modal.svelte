<script>
  import { fade, fly } from "svelte/transition";
  import { createEventDispatcher } from "svelte";

  let w;

  const dispatch = createEventDispatcher();
</script>

<style lang="scss">
  .modal-bg {
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.8);

    .modal {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-content: center;
      background: white;
      padding: 20px;
      border-radius: 15px;
      width: 50vw;
      height: 35vh;
    }
  }
</style>

<div transition:fade class="modal-bg" bind:clientWidth={w}>
  <div transition:fly={{ y: -100 }} class="modal">
    <button
      class="button slide"
      style="max-width:250px;align-self:flex-end;background:none;color:black;"
      on:click={() => {
        dispatch('close');
      }}>
      x
    </button>
    <!-- <slot>optional fallback</slot> -->
    <!-- <slot /> Generic slot -->
    <!-- <slot name="named-slot" /> -->
    <slot />
  </div>
</div>
