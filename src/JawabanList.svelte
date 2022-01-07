<script>
  import Jawaban from "./Jawaban.svelte";

  export let listJawab;
  export let correct;
</script>

<div class="jawabList">
  {#each listJawab as jawab, index (index + jawab)}
    <Jawaban {correct} {jawab} />
  {/each}
</div>

<style>
  .jawabList {
    font-family: "Open Sans", sans-serif;
    font-size: 16px;
    letter-spacing: 2px;
    text-decoration: none;
    text-transform: uppercase;
    width: 50%;
    margin: 0 auto;
    color: #000;
    cursor: pointer;
    border: 3px solid;
    padding: 0.25em 0.5em;
    box-shadow: 1px 1px 0px 0px, 2px 2px 0px 0px, 3px 3px 0px 0px,
      4px 4px 0px 0px, 5px 5px 0px 0px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    padding: 1rem;
  }
</style>
