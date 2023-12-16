<script lang="ts">
  import { LogStore } from "$ts/console";
  import { compileStringLog } from "$ts/console/collector";
  import { CrashReport } from "$ts/stores/crash";
  import { sleep } from "$ts/util";
  import { onMount } from "svelte";
  import { CrashPrefix, CrashViteDev } from "./ts/store";

  export let inline = false;
  let show = false;
  let log = "";

  onMount(async () => {
    await sleep(1000);
    show = true;
  });

  LogStore.subscribe(() => {
    const Log = `\n--- LOG ---\n\n${compileStringLog().reverse().join("\n")}`;
    const report = $CrashReport;
    const reportStr = report ? `${report.title}\n\n${report.body}\n` : "";
    const notice = !inline && import.meta.env.DEV ? CrashViteDev : "";
    const prefix = inline ? "" : CrashPrefix;
    log = `${prefix}${notice}${reportStr}${Log}`;
  });
</script>

<div class="state-crash" class:fullscreen={!inline}>
  {#if show}
    <textarea
      readonly
      bind:value={log}
      class:fullscreen={!inline}
      class:inline
    />
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

  textarea.inline {
    width: 100%;
    height: 100%;
  }
</style>
