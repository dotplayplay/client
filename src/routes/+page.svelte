<script>
import "../styles/home/index.css"
import "../styles/home/indexmobile.css"
import Icon from 'svelte-icons-pack/Icon.svelte';
import Biggestwin from "$lib/homecomponents/biggestwin.svelte";
import ProfileAuth from "../lib/profleAuth/index.svelte";
import { register } from 'swiper/element/bundle';
import BsQuestionCircle from "svelte-icons-pack/bs/BsQuestionCircle";
import Homeoriginals from '$lib/homecomponents/homeoriginals.svelte';
import Latestbet from '$lib/homecomponents/latestbet.svelte';
import Homeanimaton from "../lib/homecomponents/homeanimaton.svelte";
import { screen, is_open__Appp, is_open__chat } from "$lib/store/screen"
import {  onMount } from "svelte";
import { browser } from '$app/environment'
import { db} from "$lib/firebaseAuth/index"
import { doc, getDoc } from "firebase/firestore";
    
const id = browser && JSON.parse(localStorage.getItem('user'))
let profile
$:{
    id &&  onMount(async()=>{
        const docRef = doc(db, "profile", id.email);
        const docSnap = await getDoc(docRef);
        if (docSnap.exists()) {
            profile = docSnap.data()
        } else {
            console.log("No such document!");
        }
    })
}

$: $screen
$: $is_open__Appp

register();
</script>
    

{#if profile && profile.born === ''}
    <ProfileAuth />
{/if}

<div id="main-screen" class="sc-jwQYvw eRdxAb" style={`padding-left:${$is_open__Appp ? 240 : 72}px; padding-right:${$is_open__chat ? 360 : 0}px`}>
    <div class="sc-bLdqUH bPsBUR banner">
        <div class="gradient-wrap">
            <div class="swiper swiper-initialized swiper-horizontal sc-haTkiu iyCsvj">
                <swiper-container class="swiper-wrapper"
                    slides-per-view={1}
                    speed={2000}
                    loop={true},
                    autoplay={{
                    delay: 2000,
                    disableOnInteraction: false,
                    }} space-between="30"
                    >
                    <swiper-slide class="swiper-slide swiper-slide-duplicate">
                        <div class="sc-kTqLtj dnfJpJ">
                            <a href="/" class="sc-cfJLRR joQyOD">
                                <img src="https://res.cloudinary.com/dxwhz3r81/image/upload/v1704531967/image_14_bebai3.png" alt="">
                            </a>
                            <a href="/" class="sc-cfJLRR ktmMpR">
                                <img src="https://res.cloudinary.com/dxwhz3r81/image/upload/v1704532275/image_15_wsz8o2.png" alt="">
                            </a>
                            <a href="/" class="sc-cfJLRR ktmMpR">
                                <img src="https://res.cloudinary.com/dxwhz3r81/image/upload/v1704532534/image_16_l37zat.png" alt="">
                            </a>
                        </div>
                    </swiper-slide>
                    <swiper-slide>
                        <div class="sc-kTqLtj dnfJpJ">
                            <a gridnum="2" href="/lottery" class="sc-cfJLRR joQyOD">
                                <img src="https://res.cloudinary.com/dxwhz3r81/image/upload/v1704532668/image_14_1_hljqqi.png" alt="">
                            </a>
                            <a gridnum="1" href="/lottery" class="sc-cfJLRR ktmMpR">
                                <img src="https://res.cloudinary.com/dxwhz3r81/image/upload/v1704532716/image_15_1_bj6jsh.png" alt="">
                            </a>
                            <a gridnum="1" href="/lottery" class="sc-cfJLRR ktmMpR">
                                <img src="https://res.cloudinary.com/dxwhz3r81/image/upload/v1704532763/image_16_1_ggkc88.png" alt="">
                            </a>
                        </div>
                    </swiper-slide>
                </swiper-container>
            </div>
        </div>
    </div>
    <div class="sc-gFSQbh gyJkwe">
        <Homeanimaton />
        <Homeoriginals />
        <div class="screen-wrap">
            <Biggestwin />
            <Latestbet />
        </div>
    </div>
</div>

<div id="mobile-screen" class="sc-gFSQbh iDnJIm">
    <div class="sc-jibziO bYDJIH banner gradient-mobile ">
        <div class="gradient-wrap">
            <div class="swiper swiper-initialized swiper-horizontal swiper-ios sc-cfJLRR bOeOZi">
                <swiper-container class="swiper-wrapper"
                    slides-per-view={1}
                    speed={2000}
                    loop={true}
                    autoplay={{
                    delay: 2000,
                    disableOnInteraction: false,
                    }} space-between="30"
                    >
                    <swiper-slide class="swiper-slide swiper-slide-duplicate">
                        <div class="sc-haTkiu dxHxHL">
                            <a href="/" class="sc-jCHUfY eGrXvR">
                                <img src="	https://img2.nanogames.io/banner/af/c7/94/164300069949835.png" alt="">
                            </a>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="swiper-slide swiper-slide-duplicate">
                        <div class="image-content">
                            <a href="/" class="sc-jCHUfY eGrXvR">
                                <img src="https://img2.nanogames.io/banner/cf/56/a5/164300091137615.png" alt="">
                            </a>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="swiper-slide swiper-slide-duplicate">
                        <div class="image-content">
                            <a href="/" class="sc-jCHUfY eGrXvR">
                                <img src="https://img2.nanogames.io/banner/58/3b/b1/164300088905192.png" alt="">
                            </a>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="swiper-slide swiper-slide-duplicate">
                        <div class="image-content">
                            <a href="/" class="sc-jCHUfY eGrXvR">
                                <img src="https://img2.nanogames.io/banner/b7/6d/13/164300094200682.png" alt="">
                            </a>
                        </div>
                    </swiper-slide>
                </swiper-container>
            </div>
        </div>
    </div>

    <div class="sc-gFSQbh blNkCs">
        <div class="sc-eldieg elBGFt">
            <button class="mobile-input-enter">
                <svg xmlns:xlink="http://www.w3.org/1999/xlink" class="sc-gsDKAQ hxODWG icon">
                    <use xlink:href="#icon_Search"></use>
                </svg>
                <p>Game name | Provider | Category Tag</p>
            </button>
        </div>

        <div class="sc-iRFsWr dGbYFZ" style="height: auto;">
            <div class="sc-aaqME jiYpQl">
                <div class="sc-ihINtW cvKYOe sc-eSxRXt fLGcZr mobile-top-swiper">
                    <div class="sc-cxpSdN kQfmQV tabs">
                        <div class="tabs-navs">
                            <button class="tabs-nav is-active">
                                <div class="sc-cxVPaa jPPoTb">
                                    <div class="top">
                                        <div class="circle">
                                            <img alt="logo" src="https://static.nanogames.io/assets/bigprofit.ae9b1ce1.png">
                                        </div>
                                        <div class="word">
                                            <p><span style="color: rgb(231, 11, 108);">Much</span>Wow Wins</p>
                                        </div>
                                    </div>
                                </div>
                            </button>
                            <button class="tabs-nav">
                                <div class="sc-cxVPaa jPPoTb">
                                    <div class="top">
                                        <div class="circle">
                                            <img alt="logo" src="https://static.nanogames.io/assets/topprofit.bc94f362.png">
                                        </div>
                                        <div class="word">
                                            <p><span style="color: rgb(245, 192, 31);">Top</span>Winning Games</p>
                                        </div>
                                    </div>
                                </div>
                            </button>
                            <div class="bg is-reverse" style="left: 0%; right: 50%;"></div>
                        </div>
                        <div class="swiper swiper-initialized swiper-horizontal swiper-pointer-events">
                            <swiper-container class="swiper-wrapper"
                                slides-per-view={1}
                                speed={2380}
                                loop={true}
                                autoplay={{
                                delay: 1200,
                                disableOnInteraction: false,
                                }} space-between="30"
                                >
                                <swiper-slide class="swiper-slide swiper-slide-duplicate swiper-slide-duplicate-active">
                                    <div class="mobile-top-games-wrap">
                                        <div class="item-wrap">
                                            <div class="sc-bnOPBZ gZglJR win-game-item">
                                                <div class="sc-cxVPaa gPcmgp left">
                                                    <div class="image-inner">
                                                        <img alt="logo" src="https://img2.nanogames.io/game/image/5ab9c93b-8f99-4ff8-94ae-e412357578a6.png">
                                                    </div>
                                                </div>
                                                <div class="right">
                                                    <div class="right-word-wrap">
                                                        <p class="sp">ENEMYDOWN</p>
                                                    </div>
                                                    <div class="right-word-wrap big-word">
                                                        <p title="Won: $1131.36">Won:<span>$1131.36</span></p>
                                                    </div>
                                                    <div class="right-word-wrap"><p>In Crash</p></div>
                                                </div>
                                            </div>
                                        </div>
                                        <div class="item-wrap">
                                            <div class="sc-bnOPBZ gZglJR win-game-item">
                                                <div class="sc-cxVPaa gPcmgp left">
                                                    <div class="image-inner">
                                                        <img alt="logo" src="https://img2.nanogames.io/game/image/5ab9c93b-8f99-4ff8-94ae-e412357578a6.png">
                                                    </div>
                                                </div>
                                                <div class="right">
                                                    <div class="right-word-wrap">
                                                        <p class="sp">ENEMYDOWN</p>
                                                    </div>
                                                    <div class="right-word-wrap big-word">
                                                        <p title="Won: $1131.36">Won:<span>$1131.36</span></p>
                                                    </div>
                                                    <div class="right-word-wrap"><p>In Crash</p></div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </swiper-slide>
                                <swiper-slide class="swiper-slide swiper-slide-duplicate swiper-slide-duplicate-active">
                                    <div class="mobile-top-games-wrap">
                                        <div class="item-wrap">
                                            <div class="sc-bnOPBZ gZglJR win-game-item">
                                                <div class="sc-cxVPaa gPcmgp left">
                                                    <div class="image-inner">
                                                        <img alt="logo" src="https://img2.nanogames.io/game/image/5ab9c93b-8f99-4ff8-94ae-e412357578a6.png">
                                                    </div>
                                                </div>
                                                <div class="right">
                                                    <div class="right-word-wrap">
                                                        <p class="sp">ENEMYDOWN</p>
                                                    </div>
                                                    <div class="right-word-wrap big-word">
                                                        <p title="Won: $1131.36">Won:<span>$1131.36</span></p>
                                                    </div>
                                                    <div class="right-word-wrap"><p>In Crash</p></div>
                                                </div>
                                            </div>
                                        </div>
                                        <div class="item-wrap">
                                            <div class="sc-bnOPBZ gZglJR win-game-item">
                                                <div class="sc-cxVPaa gPcmgp left">
                                                    <div class="image-inner">
                                                        <img alt="logo" src="https://img2.nanogames.io/game/image/5ab9c93b-8f99-4ff8-94ae-e412357578a6.png">
                                                    </div>
                                                </div>
                                                <div class="right">
                                                    <div class="right-word-wrap">
                                                        <p class="sp">ENEMYDOWN</p>
                                                    </div>
                                                    <div class="right-word-wrap big-word">
                                                        <p title="Won: $1131.36">Won:<span>$1131.36</span></p>
                                                    </div>
                                                    <div class="right-word-wrap"><p>In Crash</p></div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </swiper-slide>
                            </swiper-container>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="sc-jYmNlR jjBLrt sc-emDsmM CqKVI">
            <div class="sc-ekrjqK ONlhR">
                <div class="sc-jibziO gXaUJh nav-tit">
                    <div class="cont-txt ">BA <b>IN-HOUSE</b><br>GAMES</div>
                </div>
            </div>
            <div class="sc-bjeSbO gqCCHE grid-list">
                <div class="sc-gfqkcP epfPPG bot-view super-block  game-crash">
                    <a class="sc-hKTqa gJEGaM game-item-wrap " href="/crash">
                        <div class="lazy-img img">
                            <img src="https://img2.nanogames.io/game/image/c405f953-f7ca-4da5-8309-dcba4fc44e7d.png" alt="">
                        </div>
                        <div class="hover-mask">
                            <div class="house-edge">House Edge 1%</div>
                            <svg class="play-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 63 63"><defs></defs><g fill="none" fill-rule="evenodd">
                                <circle cx="31.3" cy="31.3" r="30.3" fill="#000" fill-opacity=".2" stroke="#E5E7EE" stroke-width="2"></circle>
                                <path fill="#F5F6F7" d="M39.5 34.3l-11.3 7.5a2 2 0 01-3-1.6v-15a2 2 0 013-1.7L39.5 31a2 2 0 010 3.3z"></path>
                            </g>
                            </svg>
                        </div>
                    </a>
                    <div class="sc-fivaXQ gVplre bot-view">
                        <div class="wrap">
                            <a class="item" href="/crash">Crash</a>

                            <div class="help-btn-wrap">
                                <button>
                                    <Icon src={BsQuestionCircle}  size="18"  color="rgba(153, 164, 176, 0.6)" className="custom-icon" title="arror" />
                                </button>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="sc-gfqkcP epfPPG bot-view   mine">
                    <a class="sc-hKTqa gJEGaM game-item-wrap " href="/classic-dice">
                        <div class="lazy-img img">
                            <img src="https://img2.nanogames.io/game/image/48c4ac4d-8e93-4ad4-af48-695fa8f5397e.png" alt="">
                        </div>
                        <div class="hover-mask">
                            <div class="house-edge">House Edge 1%</div>
                            <svg class="play-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 63 63">
                                <defs></defs>
                                <g fill="none" fill-rule="evenodd">
                                    <circle cx="31.3" cy="31.3" r="30.3" fill="#000" fill-opacity=".2" stroke="#E5E7EE" stroke-width="2"></circle>
                                    <path fill="#F5F6F7" d="M39.5 34.3l-11.3 7.5a2 2 0 01-3-1.6v-15a2 2 0 013-1.7L39.5 31a2 2 0 010 3.3z"></path>
                                </g>
                            </svg>
                        </div>
                    </a>
                    <div class="sc-fivaXQ gVplre bot-view">
                        <div class="wrap">
                            <a class="item" href="/classic-dice">Classic Dice</a>
                            <div class="help-btn-wrap">
                                <button>
                                    <Icon src={BsQuestionCircle}  size="18"  color="rgba(153, 164, 176, 0.6)" className="custom-icon" title="arror" />
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="sc-gfqkcP epfPPG bot-view   game-CrashTrenball">
                    <a class="sc-hKTqa gJEGaM game-item-wrap " href="/hilo">
                        <div class="lazy-img img">
                            <img src="https://img2.nanogames.io/game/image/d64c5ee5-68c0-4d7e-bf8d-0be925f378b1.png" alt="">
                        </div>
                        <div class="hover-mask">
                            <div class="house-edge">House Edge 1%</div>
                            <svg class="play-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 63 63">
                                <defs></defs>
                                <g fill="none" fill-rule="evenodd">
                                    <circle cx="31.3" cy="31.3" r="30.3" fill="#000" fill-opacity=".2" stroke="#E5E7EE" stroke-width="2"></circle>
                                    <path fill="#F5F6F7" d="M39.5 34.3l-11.3 7.5a2 2 0 01-3-1.6v-15a2 2 0 013-1.7L39.5 31a2 2 0 010 3.3z"></path>
                                </g>
                            </svg>
                        </div>
                    </a>
                    <div class="sc-fivaXQ gVplre bot-view">
                        <div class="wrap">
                            <a class="item" href="/hilo">Hilo</a>
                            <div class="help-btn-wrap">
                                <button>
                                    <Icon src={BsQuestionCircle}  size="18"  color="rgba(153, 164, 176, 0.6)" className="custom-icon" title="arror" />
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="sc-gfqkcP epfPPG bot-view   game-CrashTrenball">
                    <a class="sc-hKTqa gJEGaM game-item-wrap " href="/mines">
                        <div class="lazy-img img">
                            <img src="https://img2.nanogames.io/game/image/0aa3d807-0380-4f8e-b65e-3179d4af2234.png" alt="">
                        </div>
                        <div class="hover-mask">
                            <div class="house-edge">House Edge 1%</div>
                            <svg class="play-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 63 63">
                                <defs></defs>
                                <g fill="none" fill-rule="evenodd">
                                    <circle cx="31.3" cy="31.3" r="30.3" fill="#000" fill-opacity=".2" stroke="#E5E7EE" stroke-width="2"></circle>
                                    <path fill="#F5F6F7" d="M39.5 34.3l-11.3 7.5a2 2 0 01-3-1.6v-15a2 2 0 013-1.7L39.5 31a2 2 0 010 3.3z"></path>
                                </g>
                            </svg>
                        </div>
                    </a>
                    <div class="sc-fivaXQ gVplre bot-view">
                        <div class="wrap">
                            <a class="item" href="/mines">Mines</a>
                            <div class="help-btn-wrap">
                                <button>
                                    <Icon src={BsQuestionCircle}  size="18"  color="rgba(153, 164, 176, 0.6)" className="custom-icon" title="arror" />
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="sc-ckRZPU iBmEfj">
                    <div class="bg-img"></div>
                </div>
            </div>
        </div>

    

            <div style="margin-top: 0.875rem;" class="sc-gsFzgR fjPUUh">
                <div class="sc-cxpSdN kQfmQV tabs sc-cAhXWc fufAIq">
                    <div class="tabs-navs">
                        <button class="tabs-nav is-active">Latest bets</button>
                        <button class="tabs-nav">Contest</button>
                        <div class="bg" style="left: 0%; right: 50%;"></div>
                    </div>
                    <div class="tabs-view" style="transform: none;">
                        <div class="sc-hmvnCu emIWso">
                            <table class="sc-gWXbKe iUeetX table is-hover">
                                <thead>
                                    <tr>
                                        <th>Game</th>
                                        <th>Player</th>
                                        <th>Payout</th>
                                        <th class="m-width">Profit</th>
                                    </tr>
                                </thead>
                            </table>
                            <tbody>
                                <tr>
                                    <td class="game-name">
                                        <img src="https://static.nanogames.io/assets/Limbo.011b8b65.png" class="game-icon" alt="">
                                        <div class="name">Limbo</div>
                                    </td>
                                    <td>
                                        <a class="sc-jUosCB iTDswZ user-info " href="/">
                                            <div class="name">Goombas™</div>
                                        </a>
                                    </td>
                                    <td>0.00x</td>
                                    <td class="lose">
                                        <div class="sc-Galmp erPQzq coin notranslate has-sign">
                                            <img class="coin-icon" alt="" src="	https://assets.coingecko.com/coins/images/1/large/bitcoin.png?1547033579">
                                            <div class="amount">
                                                <span class="amount-str">0.192884<span class="suffix">00</span></span>
                                            </div>
                                        </div>
                                    </td>
                                </tr>
                            </tbody>
                        </div>
                    </div>
                </div>
            </div>
       

    </div>
</div>
     
    
<style>
.gyJkwe .screen-wrap {
    max-width: 1368px;
    margin: 0px auto;
    padding: 1.25rem 0.625rem;
}
.iBmEfj .bg-img {
    padding-top: 100%;
    border-radius: 1.25rem;
    transform: translateZ(0px);
    position: relative;
    background-color: rgba(0, 0, 0, 0.317);
    overflow: hidden;
    background-image: url(https://res.cloudinary.com/dxwhz3r81/image/upload/v1697848358/dpp-favic_bh8fwz.png);
    background-repeat: no-repeat;
    background-position: center center;
    background-size: 32%;
}


</style>