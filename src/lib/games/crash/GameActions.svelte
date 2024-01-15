<script>
  import Icon from 'svelte-icons-pack/Icon.svelte';
  import AiOutlineQuestionCircle from "svelte-icons-pack/ai/AiOutlineQuestionCircle";
  import { screen } from "$lib/store/screen";
  import CrashInfoDialog from "./dialogs/GameInfoDialog.svelte";
  import LiveStats from "./dialogs/LiveStats.svelte";
  import RiMapGuideFill from "svelte-icons-pack/ri/RiMapGuideFill";
  import BiSolidKeyboard from "svelte-icons-pack/bi/BiSolidKeyboard";
  $: dialogData = null;
  $: showingStats = false;
</script>

{#if Boolean(dialogData)}
  <CrashInfoDialog
    launchConf={dialogData}
    on:close={() => (dialogData = null)}
  />
{/if}
{#if showingStats}
  <LiveStats on:close={() => (showingStats = false)} />
{/if}
<div class="game-actions">
  {#if $screen > 660}
    <button
      on:click={() => {
        dialogData = {
          startScreen: "Hot keys",
        };
      }}
      class="action-item">
      <Icon src={BiSolidKeyboard}  size="23"  color={`rgba(153, 164, 176, 0.6)`} title="Hot keys" />
      </button>
  {/if}
  <button on:click={() => (showingStats = true)} class="action-item">
    <Icon src={RiMapGuideFill}  size="23"  color={`rgba(153, 164, 176, 0.6)`} title="Live stat" />
    </button
  ><button
    on:click={() => {
      dialogData = {
        startScreen: "Help",
      };
    }}
    class="action-item"
    >
    <Icon src={AiOutlineQuestionCircle}  size="23"  color={`rgba(153, 164, 176, 0.6)`} title="Help" />
    </button
  >
</div>

<style>
  .game-actions {
    display: flex;
    order: 10;
    -webkit-box-align: center;
    align-items: center;
    height: 4rem;
    position: relative;
  }
  .game-actions::before {
    content: "";
    flex: 1 1 0%;
  }
  .action-item:hover {
    background: rgba(49, 52, 60, 0.35);
  }

  .action-item {
    cursor: pointer;
    margin-right: 0.5rem;
    width: 2.75rem;
    height: 2.75rem;
    border-radius: 50%;
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    -webkit-box-pack: center;
    justify-content: center;
  }
  .game-actions::after {
    content: "";
    position: absolute;
    left: 0px;
    top: 0px;
    right: 0px;
    height: 1px;
    opacity: 0.3;
    background-color: rgb(49, 52, 60);
  }
</style>
