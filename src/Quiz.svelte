<script>
  import { fly } from "svelte/transition";
  import { onMount, beforeUpdate, afterUpdate, onDestroy } from "svelte";
  import Question from "./Question.svelte";
  import Modal from "./Modal.svelte";
  import { score } from "./store.js";
  let activeQuestion = 0;

  let isModalOpen = false;

  let quiz = getQuiz();

  // This is called whenever a component has mounted.
  onMount(() => {
    console.log("I mounted");
  });
  beforeUpdate(() => {
    console.log("Before Update");
  });
  afterUpdate(() => {
    console.log("After Update");
  });

  async function getQuiz() {
    const res = await fetch(
      "https://opentdb.com/api.php?amount=10&category=15&type=multiple"
    );
    const quiz = await res.json();
    return quiz;
  }

  function nextQuestion() {
    activeQuestion += 1;
  }

  function resetQuiz() {
    isModalOpen = false;
    score.set(0);
    activeQuestion = 0;
    quiz = getQuiz();
  }

  // function addToScore() {
  //   score.set($score + 1);
  // }

  // Reactive Statement
  $: if ($score > 7) {
    isModalOpen = true;
  }

  // Reactive Declaration
  $: questionNumber = activeQuestion += 1;
</script>

<style>
  .fade-wrapper {
    display: flex;
    flex-direction: column;
  }

  .container {
    min-height: 500px;
    display: flex;
    flex-direction: column;
  }
</style>

<div>

  <button class="button slide" on:click={resetQuiz}>Start New Quiz</button>

  <h3>My Score: {$score}</h3>
  <h4>Question #{questionNumber}</h4>

  <div class="container">
    {#await quiz}
      Loading...
    {:then data}

      {#each data.results as question, index}
        {#if index === activeQuestion}
          <div in:fly={{ x: 100 }} out:fly={{ x: -200 }} class="fade-wrapper">
            <Question {nextQuestion} {question} />
          </div>
        {/if}
      {/each}

    {/await}
  </div>

</div>

{#if isModalOpen}
  <Modal on:close={resetQuiz}>
    <h2>You won!</h2>
    <p>Congratulations</p>
    <button class="button slide" on:click={resetQuiz}>Start Over</button>
  </Modal>
{/if}
