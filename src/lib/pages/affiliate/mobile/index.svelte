<script>
import Icon from 'svelte-icons-pack/Icon.svelte';
import RiSystemArrowRightSLine from "svelte-icons-pack/ri/RiSystemArrowRightSLine";
import CgFileDocument from "svelte-icons-pack/cg/CgFileDocument";
import CgLoadbarDoc from "svelte-icons-pack/cg/CgLoadbarDoc";
import BsCircleSquare from "svelte-icons-pack/bs/BsCircleSquare";

import TiClipboard from "svelte-icons-pack/ti/TiClipboard";
import { handleisLoggin } from "$lib/store/profile";
import { error, Handleis_activated , affilliate_info} from "../main/store/index";
import IoCloseSharp from "svelte-icons-pack/io/IoCloseSharp";
import { createEventDispatcher } from 'svelte';
import Terms from '../component/terms.svelte';
import Rules from '../component/rules.svelte';
import UsdRules from '../component/usd_rules.svelte';
import Home from './home.svelte';
import { handleAuthToken } from "$lib/store/routes"
import { ServerURl } from "$lib/backendUrl"
const URL = ServerURl()
import axios from "axios";
import { goto } from "$app/navigation"

const dispatch = createEventDispatcher()

let code ;
let affiilate_link ;
function handleCopyCode() {
    navigator.clipboard.writeText(code)
    .then(() => {
    error.set('Text copied to clipboard');
    setTimeout(()=>{
        error.set("")
},4000)
})
.catch((err) => {
    error.set('Unable to copy text: ', err);
    setTimeout(()=>{
        error.set("")
    },4000)
});
}

$:{
    code = $affilliate_info.affiliate_code
    affiilate_link = `${URL}/i-${$affilliate_info.affiliate_code}-n/`
}

function handleCopyLink() {
    navigator.clipboard.writeText(affiilate_link)
        .then(() => {
        error.set('Text copied to clipboard');
        setTimeout(()=>{
            error.set("")
        },4000)
        })
        .catch((err) => {
            setTimeout(()=>{
                error.set("")
            },4000)
        error.set('Unable to copy text: ', err);
    });
}

let terms = false
let is_display = false
let usd_rule = false
const handlePopRule = ((event)=>{
    if(event === 1){
        terms = true
        usd_rule = false
    }
    else if(event === 3){
        terms = false
        usd_rule = true
    }
    else{
        usd_rule = false
        terms = false
    }
    is_display = !is_display
})

const handleFetchAffilateProfile = (async()=>{
    await axios.get(`${URL}/api/affiliate`, {
        headers:{
            Authorization: `bearer ${$handleAuthToken}`
        }
    })
    .then((response)=>{
        affilliate_info.set(response.data[0])
        Handleis_activated.set(response.data[0].is_activated)
    })
    .catch((err)=>{
        setTimeout(()=>{
        error.set("")
    },4000)
        console.log(err.response.data.error)
    }
    )
})


$handleisLoggin && handleFetchAffilateProfile()


const handleCreateReferral = (async()=>{
    if(!$handleisLoggin){
        error.set('You need to login first');
        setTimeout(()=>{
            goto("/login")
            error.set("")
        },4000)
    }else{
        await axios.post(`${URL}/api/affiliate/activate`, {
            data : 1
        },{
        headers:{
            Authorization: `bearer ${$handleAuthToken}`
        }
    })
    .then((response)=>{
        Handleis_activated.set(true)
    })
    .catch((err)=>[
        console.log(err)
    ])
    }
})





</script>

    <div class="mobile">


{#if $error}
    <div class="error-message">
        <div class="hTTvsjh"> 
            <div>{$error}</div>
        </div>
    </div>
 {/if}   

 {#if is_display}
<div class="sc-bkkeKt kBjSXI" style="opacity: 1;">
    <div class="dialog casino-affiliate-terms" style="opacity: 1; transform: scale(1) translateZ(0px);">
        <div class="dialog-head has-close">
            {#if terms && !usd_rule}
                <div class="dialog-title">Affiliate Program Rules</div>
                {:else if !terms && !usd_rule}
                <div class="dialog-title">Commissions Rules</div>
                {:else}
                <div class="dialog-title">USD Rewards Rule</div>
            {/if}
        </div>
        <button on:click={handlePopRule} class="sc-ieecCq fLASqZ close-icon dialog-close">
            <Icon src={IoCloseSharp}  size="18"  color="rgb(255, 255, 255)" className="custom-icon" />
        </button>
        <div class="dialog-body default-style casino-affiliate-terms" style="z-index: 2; transform: none;">
            {#if terms && !usd_rule}
                <Terms />
            {:else if !terms && !usd_rule}
                <Rules />
                {:else}
                <UsdRules />
            {/if}
        </div>
    </div>
</div>
{/if}


        <div class="sc-bvFjSx fHLJnX welcome">
            <div class="sc-cQMzAB bBIfBG casino-header">
                <div class="header-sub flex-center">
                    <div class="left flex-center">
                        <button on:click={()=>handlePopRule(2)} class="m-item rules">
                            <Icon src={CgFileDocument} size="18" className="sc-gsDKAQ hxODWG icon" />
                            <span>Rules</span>
                        </button>
                        <button on:click={()=>handlePopRule(1)} class="m-item terms">
                            <Icon src={BsCircleSquare} size="18" className="sc-gsDKAQ hxODWG icon" />
                            <span>Terms</span>
                        </button>
                    </div>
                    <div class="right flex-center"></div>
                </div>
            </div>
            <div class="banner">
                <button class="management">
                    <Icon src={CgLoadbarDoc} size="24" color="#fff" className="sc-gsDKAQ hxODWG icon" />
                </button>
            </div>
            <div class="container">
                <div class="sc-knKHOI kAMryv my-casino ">
                    {#if !$handleisLoggin || !$Handleis_activated}
                    <div class="m-casino">
                        <div class="tip ttu">Commission ready everyday<br><span class="theme">$ 100 </span>Just a referral away</div>
                        <button on:click={handleCreateReferral} class="new spec">Create Referral Code Now</button>
                    </div>
                    {:else}
                    <div class="character banner-layer"></div>
                    <div class="sc-kTqLtj kxrCcr my-casino ">
                        <div class="m-casino">
                            <div class="tip ttu">Commission ready everyday<br>
                                <span class="theme">$ 100 </span>Just a referral away</div>
                            <div class="result-item">
                                <div class="label ttu">My Referral Code</div>
                                <div class="value">
                                    <span class="maxlength">{code}</span>
                                    <button on:click={handleCopyCode} class="copy"></button>
                                </div>
                            </div>
                            <div class="result-item">
                                <div class="label ttu">My Referral Link</div>
                                <div class="value">
                                    <span class="maxlength">{affiilate_link}</span>
                                    <button on:click={handleCopyLink}  class="copy"></button>
                                </div>
                            </div>
                            <button class="new">Create More Codes</button>
                        </div>
                    </div>
                {/if}
                </div>
                {#if !$handleisLoggin}
                <div class="section why">
                   
                    <div class="title ttu">Start Earning Today</div>
                    <div class="content">
                        <div class="sc-kTqLtj jsqEAL why-casino">
                            <div class="left">
                                <div class="title theme">Build Your Own <br> Casino Club Quickly.</div>
                                <div class="desc">It's hard to build a casino, but you can start from managing your own table on DOTPLAYPLAYIO.</div>
                                <div class="desc">
                                    <span class="theme">Dotplayplay.io</span> is not just games, it’s a platform to realize the potential of your hidden dreams. Join DOTPLAYPLAYIO and set sail on a new chapter in your wealth journey immediately!</div>
                            </div>
                            <div class="right">
                                <div class="title theme">Build A Casino Website <br> With Your Own Domain.</div>
                                <div class="desc">If you got your own plan. you can set up a casino website with your own domain, design style and theme. If you are capable to invite players and their wager amount reaches a billion dollars and above, you will be able to get your own customized casino!</div>
                                <div class="desc">Contact
                                    <a href="mailto:support@dotplayplay.io" class="theme">support@dotplayplay.io</a> for more details</div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="section rewards-system">
                    <div class="title ttu">
                        <span class="theme">Affiliate</span>
                        Reward System</div>
                    <div class="tip">DOTPLAYPLAY.IO sets up a reward of 100 USD for each referral you invite in addition to commission.
                        Click <span>"Create Referral Code Now"</span>
                        and set sail on a new chapter on your journey of wealth immediately!</div>
                </div>

                <div class="section">
                    <div class="sc-haTkiu fgzCdg rewards-graph">
                        <div class="title">Affiliate Rewards</div>
                        <div class="rewards-wrap">
                            <a href="/#" class="item-rewards">
                                <div class="type ttu">USD Rewards</div>
                                <div class="tip-detail">Click for more details</div>
                            </a>
                            <a href="/#" class="item-commission">
                                <div class="type">Commission Rewards</div>
                                <div class="tip-detail">Click for more details</div>
                            </a>
                        </div>
                    </div>
                </div>

                <div class="section">
                    <div class="title ttu">Affiliate Rewards</div>
                    <div class="content">
                        <div class="sc-cfJLRR cdwmLq rewards-wrap">
                            <div class="rewards item">
                                <div class="system" style="background-image: url(&quot;https://static.nanogames.io/assets/rewards.dadef713.png&quot;);">
                                    <div class="title theme ttu">USD Rewards</div>
                                    <div class="desc">Every friend you invite will get you</div>
                                    <div class="flex">
                                        <div class="amount">100 USD</div>
                                        <a href="/#" class="hover theme">USD Rewards Rules</a>
                                        <Icon src={RiSystemArrowRightSLine} color="rgb(245, 246, 247)" size="18" />
                                    </div>
                                </div>

                                <div class="graph" id="system-rewards" ></div>
                                <div class="footer">
                                    <p class="text">Please contact us for a more profitable customized plan.</p>
                                    <a href="https://t.me/NanoGamesOfficial" target="_blank" class="contact">
                                        <div class="icon-box">
                                            <svg xmlns:xlink="http://www.w3.org/1999/xlink" class="sc-gsDKAQ hxODWG icon icon">
                                                <use xlink:href="#icon_Send"></use>
                                            </svg>
                                        </div>
                                        <span>Contact Us</span>
                                    </a>
                                </div>
                            </div>
                            <div class="commission item">
                                <div class="system" style="background-image: url(&quot;https://static.nanogames.io/assets/commission.62eb3f82.png&quot;);">
                                    <div class="title theme ttu">Commission Rewards</div>
                                    <div class="desc">Every friend you invite will rebate you a percentage of their wagers as your commission and will be credited directly to your balance.</div>
                                </div>
                                <div class="graph" id="system-commission"></div>
                                <div class="footer"></div>
                            </div>
                        </div>
                    </div>
                    
                </div>
                {/if}
           
                {#if $handleisLoggin}
                <div class="container">
                    <Home on:open={()=>handlePopRule(3)}/>
                </div>
                {/if}

                <div class="section">
                    <div class="sc-bLdqUH eoJPQL platform-rewards">
                        <div class="is-mobile">
                            <div class="title ttu">Rewards sent out till date</div>
                            <div class="fc">
                                <div class="rewards">
                                    <div class="desc">USD rewards sent out till date</div>
                                    <div class="number-wrap">
                                        <div class="value">129855.5</div>
                                        <div class="type">USD</div>
                                    </div>
                                </div>
                                <div class="commission">
                                    <div class="desc">Commission sent out till date</div>
                                    <div class="number-wrap">
                                        <div class="value">500323.79</div>
                                        <div class="type">USD</div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                {#if !$handleisLoggin}
                <button class="sc-iqseJM sc-egiyK cBmlor fnKcEH button button-normal button">
                    <div class="button-inner">Create Referral Code Now</div>
                </button>
                {/if}
            </div>
        </div>
    </div>

<style>
.dialog {
    position: absolute;
    display: flex;
    flex-direction: column;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    margin: 0;
    transition-property: width, height, margin-left, margin-top;
    transition-duration: 0.5s;
    border-radius: 1.25rem;
    overflow: hidden;
    background-color: rgb(23, 24, 27);
}

.kAMryv {
    width: 100%;
    height: auto;
    padding: 0px 1.6875rem;
    background-image: linear-gradient(rgb(163, 20, 220), rgb(110, 4, 164) 88%, transparent 88%);
    margin-bottom: 2.5rem;
    box-sizing: border-box;
    position: relative;
    margin: 0px auto;
}
.kAMryv .m-casino {
    width: 100%;
    height: 416px;
    border-radius: 20px;
    background-image: linear-gradient(rgb(159, 31, 244), rgb(62, 14, 95));
    padding: 106px 32px 0px;
    box-sizing: border-box;
    position: relative;
}
.kAMryv .m-casino::before {
    content: "";
    width: 100%;
    height: 106px;
    position: absolute;
    left: 0px;
    top: 0px;
    background: url(https://static.nanogames.io/assets/my-casino.925e409c.png) center 20px / 176px no-repeat;
}
.kAMryv .tip {
    font-size: 16px;
    color: rgb(255, 255, 255);
    font-weight: 600;
    margin-bottom: 12px;
    white-space: nowrap;
    line-height: 1.5;
}
.kAMryv .result-item {
    font-size: 14px;
    margin-bottom: 0.75rem;
    color: rgb(255, 255, 255);
}
.kAMryv .label {
    color: rgb(255, 209, 12);
    padding: 0px 18px;
}
.kAMryv .value {
    height: 44px;
    border-radius: 22px;
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    background: rgba(68, 14, 105, 0.5);
    padding: 0px 18px;
}
.kAMryv .maxlength {
    flex: 0 1 93%;
    overflow: hidden;
    white-space: nowrap;
    opacity: 0.7;
    user-select: text;
}
.kAMryv .copy {
    background: url(https://static.nanogames.io/assets/copy.37dd4904.svg) center center / auto 18px no-repeat;
    width: 18px;
    height: 18px;
}

</style>