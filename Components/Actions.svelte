<script lang="ts">
  export let moreInfo: boolean;

  function toggle() {
    moreInfo = !moreInfo;
  }

  function restart() {
    location.reload();
  }
</script>

<div class="actions">
  <button on:click={toggle}>{moreInfo ? "Go Back" : "More Info"}</button>
  <button class="restart" on:click={restart}>Restart</button>
</div>
