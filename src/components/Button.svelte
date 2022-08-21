<script lang="ts">
  export let style: string = "primary";
  export let type: string = "button";
  export let disabled: boolean = false;
</script>

<div class="btn-container">
  <button {type} {disabled} class={style}>
    <slot />
  </button>
</div>

<style>
  button {
    color: #fff;
    border: 0;
    border-radius: 8px;
    color: #fff;
    width: 100%;
    height: 40px;
    cursor: pointer;
    margin-top: 10px;
  }

  .primary {
    background-color: #202142;
  }

  .secondary {
    background: #ff6a95;
  }

  button:hover {
    transform: scale(0.98);
    opacity: 0.9;
  }

  button:disabled {
    background-color: #cccccc;
    color: #333;
    cursor: auto;
  }

  button:disabled:hover {
    transform: scale(1);
    opacity: 1;
  }

  @media screen and (min-width: 768px) {
    .btn-container {
      display: flex;
      justify-content: flex-end;
    }
    button {
      width: 100px;
    }
  }
</style>
