<script lang="ts">
  import ProcessRenderer from "$state/Desktop/Components/ProcessRenderer.svelte";
  import { ProcessHandler } from "$ts/process";
  import { sleep } from "$ts/util";
  import { onMount } from "svelte";
  import Actions from "./Components/Actions.svelte";
  import Content from "./Components/Content.svelte";
  import ViteNotice from "./Components/ViteNotice.svelte";
  import MoreInfo from "./Crash/MoreInfo.svelte";
  import "./css/main.css";

  let moreInfo = false;
  let show = false;
  let handler = new ProcessHandler("Crash");

  onMount(async () => {
    await sleep(500);
    show = true;
  });
</script>

<div class="top" class:show>
  {#if !moreInfo}
    <Content bind:moreInfo />
  {:else}
    <MoreInfo />
  {/if}
</div>
<div class="bottom" class:show class:more-info={moreInfo}>
  {#if moreInfo}
    <ViteNotice />
    <div class="actions-wrapper">
      <Actions bind:moreInfo />
    </div>
  {/if}
</div>
<ProcessRenderer {handler}></ProcessRenderer>
