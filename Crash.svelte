<script lang="ts">
  import "./css/main.css";
  import Actions from "./Components/Actions.svelte";
  import Content from "./Components/Content.svelte";
  import ViteNotice from "./Components/ViteNotice.svelte";
  import MoreInfo from "./Crash/MoreInfo.svelte";
  import { onMount } from "svelte";
  import { sleep } from "$ts/util";

  let moreInfo = false;
  let show = false;

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
  <div class="actions-wrapper" />
  <ViteNotice />
  <div class="actions-wrapper">
    {#if moreInfo}
      <Actions bind:moreInfo />
    {/if}
  </div>
</div>
