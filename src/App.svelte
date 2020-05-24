<script>
  import Quiz from "./Quiz.svelte";
</script>

<style>
  :global(body) {
    background: #524763;
  }

  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: white;
    text-align: center;
  }

  div {
    background: white;
    border-radius: 15px;
    padding: 40px;
    max-height: 75vh;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  :global(.button) {
    border-radius: 4px;
    border: 0;
    color: #fff;
    cursor: pointer;
    padding: 15px 20px;
    font-size: 18px;
    font-weight: 400;
    line-height: 22px;
    margin-right: 15px;
  }

  /* Slide */
  :global(.slide) {
    background-color: #008b73;
    transform: perspective(1px) translateZ(0);
  }

  :global(.slide:before) {
    content: "";
    position: absolute;
    z-index: -1;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #00c2a7;
    border-radius: 2px;
    transform: scaleX(0);
    transform-origin: 0 50%;
    transition-property: transform;
    transition-duration: 0.3s;
    transition-timing-function: ease-out;
  }

  :global(.slide:hover::before) {
    transform: scaleX(1);
  }
</style>

<main>
  <h1>Level Up Quiz</h1>
  <div>
    <Quiz />
  </div>
</main>
