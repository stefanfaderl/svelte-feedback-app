<script lang="ts">
  import { createEventDispatcher } from "svelte";

  let selected: number = 10;

  const dispatch = createEventDispatcher();

  const onChange = (event) => {
    selected = event.currentTarget.value;
    dispatch("rating-select", selected);
  };
</script>

<ul class="rating">
  {#each [...new Array(10)].map((_, i) => i + 1) as rating}
    <li>
      <input
        type="radio"
        id={`num${rating}`}
        name="rating"
        value={rating}
        on:change={onChange}
        checked={selected === rating}
      />
      <label for={`num${rating}`}>{rating}</label>
    </li>
  {/each}
</ul>

<style>
  .rating {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    margin: 30px 0;
  }

  .rating li {
    position: relative;
    background: #f4f4f4;
    width: 50px;
    height: 50px;
    padding: 10px;
    text-align: center;
    border-radius: 50%;
    font-size: 19px;
    border: 1px #eee solid;
    transition: 0.3s;
    margin: 5px;
  }

  .rating li label {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 50px;
    height: 50px;
    padding: 10px;
    border-radius: 50%;
    transform: translate(-50%, -50%);
    cursor: pointer;
  }

  .rating li:hover {
    background: #ff6a95;
    color: #fff;
  }

  /* Make actual radio select invisible */
  [type="radio"] {
    opacity: 0;
  }

  /* Use the sibling select */
  [type="radio"]:checked ~ label {
    background: #ff6a95;
    color: #fff;
  }
</style>
