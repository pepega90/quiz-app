<script>
  import { setContext } from "svelte";
  import data from "./store";
  import Tanya from "./Tanya.svelte";
  import JawabanList from "./JawabanList.svelte";

  let question = {};
  let list = data;
  let idx = 0;
  let next = false;
  let correct = "";
  let done = false;  
  let score = 0;


  question = list[idx];
  

  function checkJawaban(answer) {
    if (question.jawaban == answer && !done) score += 1;
    correct = question.jawaban;
    if (idx == list.length - 1) done = true;
    else next = true;
  }

  function nextQuestion() {
    if (idx < list.length - 1) {
      idx++;
      next = false;
    }
    correct = "";
    question = list[idx];
  }

  function restart() {
    idx = 0;
    question = list[idx];
    correct = "";
    done = false;
    next = false;
    score = 0;
  }

  setContext("check", checkJawaban);
</script>

<main>
  <h1 class="header">Quiz App</h1>
  <Tanya pertanyaan={question.tanya} />
  <JawabanList {correct} listJawab={question.listJawaban} />
  {#if next && !done}
    <button class="button-54" on:click={nextQuestion} type="button">Next</button
    >
  {/if}
  {#if done}
    <button class="button-54" on:click={restart} type="button">Restart</button>
    <h1>Score Kamu: {score} ({score}/{list.length})</h1>
  {/if}
</main>

<style>
  main {
    text-align: center;
  }

  .header {
    margin-bottom: 2em;
    color: orange;
  }

  /* CSS */
  .button-54 {
    margin-top: 2em;
    font-family: "Open Sans", sans-serif;
    font-size: 16px;
    letter-spacing: 2px;
    text-decoration: none;
    text-transform: uppercase;
    color: #000;
    cursor: pointer;
    border: 3px solid;
    padding: 0.25em 0.5em;
    box-shadow: 1px 1px 0px 0px, 2px 2px 0px 0px, 3px 3px 0px 0px,
      4px 4px 0px 0px, 5px 5px 0px 0px;
    position: relative;
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
  }

  .button-54:active {
    box-shadow: 0px 0px 0px 0px;
    top: 5px;
    left: 5px;
  }

  @media (min-width: 768px) {
    .button-54 {
      padding: 0.25em 0.75em;
    }
  }
</style>
