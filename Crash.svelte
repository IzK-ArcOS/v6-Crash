<script lang="ts">
  import { LogStore } from "$ts/console";
  import { compileStringLog } from "$ts/console/collector";
  import { CrashReport } from "$ts/stores/crash";
  import { sleep } from "$ts/util";
  import { onMount } from "svelte";

  let show = false;

  const prefix = `---! [ ArcOS crashed ] !---\n\nBelow you'll find the log, which may contain information about the crash.\nA bug report has been sent to the Reports server informing it of the crash.\n\n`;

  let log = "";

  onMount(async () => {
    await sleep(1000);
    show = true;
  });

  LogStore.subscribe(() => {
    const Log = `\n--- LOG ---\n\n${compileStringLog().join("\n")}`;
    const crashRep = $CrashReport;
    const reportStr = crashRep ? `${crashRep.title}\n\n${crashRep.body}\n` : "";
    const extra = import.meta.env.DEV
      ? "WARNING: ArcOS in Vite Development will not send Bug Reports to prevent spamming of servers.\n\n"
      : "";

    log = `${prefix}${extra}${reportStr}${Log}`;
  });
</script>

<div class="state-crash fullscreen">
  {#if show}
    <textarea readonly bind:value={log} class="fullscreen" />
  {/if}
</div>

<style scoped>
  textarea {
    border: none;
    background-color: #111;
    color: #bbb;
    font-family: "Source Code Pro", monospace;
    font-size: 14px;
    resize: none !important;
    overflow-x: hidden;
    padding: 20px;
  }
</style>
