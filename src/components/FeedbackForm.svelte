<script lang="ts">
  import { FeedbackStore } from "../stores";
  import { v4 as uuidv4 } from "uuid";
  import Button from "./Button.svelte";
  import RatingSelect from "./RatingSelect.svelte";
  import Card from "./UI/Card.svelte";

  let text: string = "";
  let btnDisabled: boolean = true;
  let min: number = 10;
  let message: string;
  let rating: number = 10;

  const handleInput = () => {
    if (text.trim().length <= min) {
      message = `Text must be at least ${min} characters`;
      btnDisabled = true;
    } else {
      message = null;
      btnDisabled = false;
    }
  };

  const handleSelect = (e: { detail: number }) => (rating = e.detail);

  const handleSubmit = () => {
    if (text.trim().length > min) {
      const newFeedback = {
        id: uuidv4(),
        text,
        rating: +rating,
      };

      FeedbackStore.update((currentFeedback) => {
        return [newFeedback, ...currentFeedback];
      });
      text = "";
    }
  };
</script>

<Card>
  <header>
    <h2>How would you rate your service with us?</h2>
  </header>
  <form on:submit|preventDefault={handleSubmit}>
    <!-- Rating Select -->
    <RatingSelect on:rating-select={handleSelect} />
    <div class="input-group">
      <input
        type="text"
        on:input={handleInput}
        bind:value={text}
        placeholder="Tell us something"
      />
    </div>
    <Button disabled={btnDisabled} type="type">Send</Button>
    {#if message}
      <div class="message">
        {message}
      </div>
    {/if}
  </form>
</Card>

<style>
  header {
    max-width: 400px;
    margin: auto;
  }

  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }

  .input-group {
    display: flex;
    border: 1px solid #ccc;
    padding: 8px 10px;
    border-radius: 8px;
    margin-top: 15px;
  }

  input {
    flex-grow: 2;
    border: none;
    font-size: 16px;
    text-align: center;
  }

  input:focus {
    outline: none;
  }

  .message {
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }

  @media screen and (min-width: 768px) {
    input {
      text-align: left;
    }
  }
</style>
