<script lang="ts">
  import { CrashReport } from "$ts/stores/crash";
  import Actions from "./Actions.svelte";

  export let moreInfo: boolean;
</script>

<div class="crash-content">
  <span class="icon material-icons-round">report</span>
  <h1 class="title">ArcOS Crashed!</h1>
  <p class="info">
    An error occured and ArcOS had to shut down. A Bug Report has been submitted, informing us of
    the crash.<br /><br />
    This session can't continue. You can choose to restart.
  </p>
  <p class="error">{$CrashReport ? $CrashReport.title : "No Crash Report!"}</p>
  <Actions bind:moreInfo />
</div>
