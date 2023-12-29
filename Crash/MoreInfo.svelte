<script lang="ts">
  import { LogStore } from "$ts/console";
  import { compileStringLog } from "$ts/console/collector";
  import { CrashReport } from "$ts/stores/crash";
  import { CrashPrefix } from "../ts/store";

  let log = "";

  LogStore.subscribe(() => {
    const Log = `\n--- LOG ---\n\n${compileStringLog().reverse().join("\n")}`;
    const report = $CrashReport;
    const reportStr = report ? `${report.title}\n\n${report.body}\n` : "";
    log = `${CrashPrefix}${reportStr}${Log}`;
  });
</script>

<div class="more-info">
  <textarea readonly bind:value={log} />
</div>

<style scoped>
  textarea {
    border: none;
    background-color: #000;
    color: #ccc;
    font-family: "Source Code Pro", monospace;
    font-size: 14px;
    resize: none !important;
    overflow-x: hidden;
    padding: 20px;
  }
</style>
