<script lang="ts">
  export let moreInfo: boolean;

  function toggle() {
    moreInfo = !moreInfo;
  }
</script>

<div class="actions">
  <button on:click={toggle}>{moreInfo ? "Go Back" : "View Logs"}</button>
  <button class="restart">Restart</button>
</div>
