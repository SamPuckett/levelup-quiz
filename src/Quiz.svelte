<script>
  let result = "";
  let correctAnswer = "b";
  let answers = ["a", "b", "c", "d"];
  let quiz = getQuiz();

  function pickAnswer(answer) {
    if (answer === correctAnswer) {
      return (result = "Correct!");
    }
    result = "OOPS!";
  }

  async function getQuiz() {
    const res = await fetch(
      "https://opentdb.com/api.php?amount=10&category=15&type=multiple"
    );
    const quiz = await res.json();
    return quiz;
  }

  function handleClick() {
    quiz = getQuiz();
  }
</script>

<div>

  <button on:click={handleClick}>Get Questions</button>

  {#if result}
    <h4>{result}</h4>
  {:else}
    <h4>Please Pick an Answer</h4>
  {/if}

  {#await quiz}
    Loading...
  {:then data}
    <h3>{data.results[0].question}</h3>
  {/await}

  {#each answers as answer}
    <button on:click={() => pickAnswer(answer)}>
      Answer {answer.toUpperCase()}
    </button>
  {/each}

</div>
