<script lang="ts">
  // import { onMount, onDestroy } from "svelte";
  import { FeedbackStore } from "../stores";
  import FeedbackItem from "./FeedbackItem.svelte";
  import { fade, scale } from "svelte/transition";

  /* longer way with subscribe */
  /*   let feedback = []; 

  const unsubscribe = FeedbackStore.subscribe((data) => {
    feedback = data;
  });

  onMount(() => {
    console.log("MOUNTED");
  });

  onDestroy(() => {
    unsubscribe();
  }); */
</script>

{#each $FeedbackStore as fb (fb.id)}
  <!-- use feedbackstore directly, it´s unsubscribes automatically -->
  <div in:scale out:fade={{ duration: 500 }}>
    <FeedbackItem item={fb} />
  </div>
{/each}
