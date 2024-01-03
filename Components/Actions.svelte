<script lang="ts">
  import { LoggerApp } from "$apps/LoggerApp/ts/app";
  import { spawnApp } from "$ts/apps";
  import { ProcessHandler } from "$ts/process";
  import { LogLevel } from "$types/console";

  export let moreInfo: boolean;
  export let handler: ProcessHandler;

  function toggle() {
    moreInfo = !moreInfo;
  }

  function viewLogs() {
    spawnApp("LoggerApp", 0, [LogLevel.error, "*"], handler, LoggerApp);
  }

  function restart() {
    location.reload();
  }
</script>

<div class="actions">
  <button on:click={viewLogs}>Open Logging</button>
  <button on:click={toggle}>{moreInfo ? "Go Back" : "More Info"}</button>
  <button class="restart" on:click={restart}>Restart</button>
</div>
