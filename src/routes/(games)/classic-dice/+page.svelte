<script>

import Gameview from "$lib/games/ClassicDice/gameview.svelte";
import "$lib/games/ClassicDice/styles/index.css"
import Controls from "$lib/games/ClassicDice/Controls.svelte";
import Icon from 'svelte-icons-pack/Icon.svelte';
import RiSystemArrowDropRightLine from "svelte-icons-pack/ri/RiSystemArrowDropRightLine";
import { onMount } from "svelte";
import { browser } from '$app/environment'
import { handleAuthToken } from "$lib/store/routes"
import { handleSoundManager } from "$lib/games/ClassicDice/audio/SoundManager"
import { soundManager, turboManager } from "$lib/games/ClassicDice/store/index";
import Allbet from "$lib/games/ClassicDice/componets/allbet.svelte";
import Mybet from "$lib/games/ClassicDice/componets/mybet.svelte";
import Hotkey from "$lib/games/ClassicDice/componets/hotkey.svelte";
import LiveStats from "$lib/games/ClassicDice/componets/liveStats.svelte";
import SeedSetting from "$lib/games/ClassicDice/componets/seedSetting.svelte";
import Help from "$lib/games/ClassicDice/componets/help.svelte";
import { soundHandler } from "$lib/games/ClassicDice/store/index"
import { handleDiceGameEncrypt } from "$lib/games/ClassicDice/hook/gameEncrypt" 
import { screen, is_open__Appp, is_open__chat } from "$lib/store/screen";
import { DiceHistory } from "$lib/games/ClassicDice/hook/diceHistory"

$: is_hotkey = false
$: is_stats = false
$: isSeed = false
$: isHelp = false
$: loading = true
$: is_allbet = true
$: is_mybet = false
$: is_contest = false

onMount(async()=>{
  const resion = $handleAuthToken && await handleDiceGameEncrypt($handleAuthToken)
  $handleAuthToken && await DiceHistory($handleAuthToken)
  const id = browser && JSON.parse(localStorage.getItem('classic_dice_sound'))
  const tubor = browser && JSON.parse(localStorage.getItem('classic_dice_tubo'))
  soundHandler.set(id)
  turboManager.set(tubor)
  soundManager.set(handleSoundManager()) 
  loading = (resion.is_loading)
})

const handleAllbet = ((e) => {
    if (e === 1) {
        is_allbet = true
        is_mybet = false
        is_contest = false
    } else if (e === 2) {
        is_allbet = false
        is_mybet = true
    } else {
        is_contest = true
        is_allbet = false
        is_mybet = false
    }
})

const handleSoundState = (()=>{
    if($soundHandler){
        soundHandler.set(null)
        localStorage.removeItem("classic_dice_sound");
    }else{
        soundHandler.set(true)
        localStorage.setItem("classic_dice_sound", true);
    }
})

const handleTurbeState = (()=>{
    if($turboManager){
        turboManager.set(null)
        localStorage.removeItem("classic_dice_tubo");
    }else{
        turboManager.set(true)
        localStorage.setItem("classic_dice_tubo", true);
    }
})

$: newScreen = 0
  $: {
    if($is_open__Appp && !$is_open__chat){
      newScreen = $screen - 240
    }
    else if(!$is_open__Appp && $is_open__chat){
      newScreen = $screen - 432
    }
    else if(!$is_open__Appp && !$is_open__chat){
      newScreen = $screen - 72
    }
    else if($is_open__Appp && $is_open__chat){
      newScreen = $screen - 600
    }
}

</script>
{#if is_hotkey}
  <Hotkey on:close={()=> is_hotkey = false} />
{/if}

{#if is_stats}
  <LiveStats on:close={()=> is_stats = false} />
{/if}

{#if isSeed}
  <SeedSetting on:close={()=> isSeed = false}/>
{/if}

{#if isHelp}
    <Help on:close={()=> isHelp = false} />
{/if}


{#if !loading}
<div id="dice-main">
    <div id="game-ClassicDice" class={`sc-haTkiu lmWKWf ${newScreen > 1000 ? "game-style0" : "game-style1" }  sc-gDGHff gYWFhf ${$is_open__Appp && `is-open`} ${$is_open__chat && `is-chat`}`}>
        <div class="game-area">
            <div class="game-main">
                <Gameview />
                <Controls />
                <div class="game-actions">
                    <button on:click={()=> handleSoundState()} class={`action-item ${$soundHandler ? "active" : ""} `}>
                        <svg xmlns:xlink="http://www.w3.org/1999/xlink" class="sc-gsDKAQ hxODWG icon">
                            <use xlink:href="#icon_SoundOn"></use>
                        </svg>
                    </button>
                    <button on:click={()=> handleTurbeState()} class={`action-item ${$turboManager ? "active" : ""}`}>
                        <svg xmlns:xlink="http://www.w3.org/1999/xlink" class="sc-gsDKAQ hxODWG icon">
                            <use xlink:href="#icon_TurboBet"></use>
                        </svg>
                    </button>
                    {#if $screen > 650}
                        <button on:click={()=> is_hotkey = true} class="action-item  ">
                            <svg xmlns:xlink="http://www.w3.org/1999/xlink" class="sc-gsDKAQ hxODWG icon">
                                <use xlink:href="#icon_HotKeys"></use>
                            </svg>
                        </button>
                    {/if}
                    <button on:click={()=> is_stats = true} class="action-item  ">
                        <svg xmlns:xlink="http://www.w3.org/1999/xlink" class="sc-gsDKAQ hxODWG icon">
                            <use xlink:href="#icon_LiveStats"></use>
                        </svg>
                    </button>
                    <button on:click={()=> isSeed = true} class="action-item  " id="set_seed">
                        <svg xmlns:xlink="http://www.w3.org/1999/xlink" class="sc-gsDKAQ hxODWG icon">
                            <use xlink:href="#icon_Seed"></use>
                        </svg>
                    </button>
                    <button on:click={()=> isHelp = true} class="action-item  ">
                        <svg xmlns:xlink="http://www.w3.org/1999/xlink" class="sc-gsDKAQ hxODWG icon">
                            <use xlink:href="#icon_Help"></use>
                        </svg>
                    </button>
                </div>
            </div>
        </div>
        <div class="sc-cxpSdN kQfmQV tabs game-tabs len-3">
            <div class="tabs-navs">
                <button on:click={()=>handleAllbet(1)} class={`tabs-nav ${is_allbet && "is-active"}`}>All Bets</button>
                <button on:click={()=>handleAllbet(2)} class={`tabs-nav ${is_mybet && "is-active"}`}>My Bets</button>
                <button on:click={()=>handleAllbet(3)} class={`tabs-nav ${is_contest && "is-active"}`}>Contest</button>
            {#if is_allbet}
                <div class="bg" style={`left: 0%; right: 66.6667%;`}></div>
            {:else if is_mybet}
                <div class="bg" style="left: 33.3333%; right: 33.3333%;"></div>
            {:else if is_contest}
                <div class="bg" style="left: 66.6667%; right: 0%;"></div>
            {/if}
            </div>
            {#if is_allbet}
            <Allbet />
            {:else if is_mybet}
            <Mybet />
            {/if}
        </div>

        <div class="sc-knKHOI cFxmZX">
            <div class="intro-title">
            <p>Classic Dice</p>
            <div class="intro-tags">
                <p>Our Best Games</p>
                <p>BC Originals</p>
                <p>Recommended Games</p>
                <p>Dice</p>
            </div>
            </div>
            <div class="description">Classic Dice, a probability game established by blockchain hash value calculation and algorithm, provides more fun with bet and prediction, in which the closer the number rolled by players to the random number, the higher the probability winning.</div>
            <button class="intro-detail">
            Details
            <span style="margin-left: 1.125rem;">
                <Icon src={RiSystemArrowDropRightLine}  size="23"  color="rgba(153, 164, 176, 0.6)"  />
            </span>
            </button>
        </div>
    </div>
</div>
{:else}
<div class="uytutfyh">
    <div class="tdthuy">
        <img src="https://res.cloudinary.com/dxwhz3r81/image/upload/v1697848286/dpp-favicon-logo_j53rwc.jpg" alt="">
    </div>
</div>
{/if}


<style>

.uytutfyh{
    background-color: var(--background-color);
    width: 100%;
    height: 100vh;
}
.tdthuy {
    display: flex;

    align-items: center;
    justify-content: center;
    align-content: center;
    height: 500px;
}
.tdthuy img{
    width: 120px;
    background-color: rgba(51, 57, 57, 0.502);
    padding: 20px;
    opacity: 0.6;
    border-radius: 50%;
    animation: monyy 3s infinite;
}


@keyframes monyy{
    10%{
        margin-right: -100px;
    }

    100%{
        margin-right: 100px;
    }
}


.ePAxUv {
    margin-top: 4rem;
}

.kQfmQV .tabs-navs {
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    height: 2.25rem;
    position: relative;
    border-radius: 1.125rem;
    background-color: rgba(49, 52, 60, 0.7);
}

.lmWKWf.is-open{
    padding-left: 50px;
}

.lmWKWf.is-chat{
    padding-right: 360px;
}

.lmWKWf .game-actions {
    display: flex;
    order: 10;
    -webkit-box-align: center;
    align-items: center;
    height: 4rem;
    position: relative;
}

.lmWKWf .game-actions::before {
    content: "";
    flex: 1 1 0%;
}

.lmWKWf .action-item {
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
 .action-item.active .icon {
    fill: rgb(67, 179, 9);
}
.action-item:hover {
    background: rgba(203, 203, 203, 0.082);
}

.lmWKWf .game-actions::after {
    content: "";
    position: absolute;
    left: 0px;
    top: 0px;
    right: 0px;
    height: 1px;
    opacity: 0.3;
    background-color: rgb(49, 52, 60);
}

.lmWKWf .game-actions::before {
    content: "";
    flex: 1 1 0%;
}

.lmWKWf .game-actions {
    display: flex;
    order: 10;
    -webkit-box-align: center;
    align-items: center;
    height: 4rem;
    position: relative;
}

.lmWKWf .game-tabs {
    margin-top: 2.5rem;
}

.lmWKWf .game-tabs .tabs-navs {
    margin-bottom: 0.75rem;
    margin-left: 0.625rem;
    display: inline-flex;
}

.lmWKWf .game-tabs .tabs-navs .tabs-nav {
    width: 5.625rem;
}

.kQfmQV .tabs-nav.is-active {
    color: rgb(245, 246, 247);
    font-weight: bold;
}

.kQfmQV .tabs-nav {
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    -webkit-box-pack: center;
    justify-content: center;
    flex: 1 1 0%;
    height: 100%;
    cursor: pointer;
    white-space: nowrap;
    width: 100%;
    z-index: 1;
}

.kQfmQV .tabs-navs .bg {
    border-radius: 1.125rem;
    background-image: linear-gradient(to left, rgb(85, 89, 102), rgb(85, 89, 102), rgb(88, 174, 20));
    opacity: 0.4;
    height: 100%;
    position: absolute;
    left: 0px;
    top: 0px;
    transition: right 0.2s ease-out 0s, left 0.3s ease-out 0s;
    transform: translateZ(0px);
    box-shadow: rgba(0, 0, 0, 0.14) 0px 0px 0.3125rem;
}
.cFxmZX {
    width: 100%;
    border-radius: 1.25rem;
    background-color: rgb(30, 32, 36);
    padding: 1.5rem 1.5rem 2rem;
    margin-top: 2rem;
}
.cFxmZX .intro-title {
    min-height: 5rem;
    display: flex;
    -webkit-box-align: center;
    align-items: center;
}
.cFxmZX .intro-title > p {
    font-size: 1rem;
    color: rgb(245, 246, 247);
    font-weight: 600;
    margin: 0px;
    white-space: nowrap;
}
.cFxmZX .intro-title .intro-tags {
    margin-left: 2.5rem;
    display: flex;
    flex-wrap: wrap;
}
.cFxmZX .intro-title .intro-tags > p {
    margin: 0px 1.125rem 0.3125rem 0px;
    padding: 0.5rem 1.25rem;
    border-radius: 1.125rem;
    background-color: rgb(43, 47, 54);
}
.cFxmZX .description {
    margin-top: 0.75rem;
    line-height: 1.25rem;
}
.cFxmZX .intro-detail {
    width: 6.75rem;
    height: 2.5rem;
    margin-top: 2rem;
    border-radius: 1.25rem;
    background-color: rgba(49, 52, 60, 0.6);
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    -webkit-box-pack: center;
    justify-content: center;
}
</style>
