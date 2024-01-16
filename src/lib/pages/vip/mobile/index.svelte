<script>
let vip = [
    {id:1, icon: "https://static.nanogames.io/assets/dice.cb7509e5.png", vipLevel:"03", nameLock: "Roll Competition", isLucked: true, content: `Try your luck once a day for a spot on our daily top 10 and win some free Doge!`},
    {id:2, icon: "https://static.nanogames.io/assets/money.9316ba83.png", vipLevel:"03", nameLock: "Tip", isLucked: true, content: `Send a little (or a lot of) luck to your friends, you’ve earned the ability to tip others.`},
    {id:3, icon: "https://static.nanogames.io/assets/rain.81aa4c59.png", vipLevel:"03", nameLock: "Raining", isLucked: true, content: `Randomly reward players in chat room every 6 hours.`},
    {id:3, icon: "https://static.nanogames.io/assets/coindrop.2d362bea.png", vipLevel:"03", nameLock: "Coindrop", isLucked: true, content: `You can now get coin drops from the chatroom for a little extra luck!`},
    {id:4, icon: "https://static.nanogames.io/assets/jpg.dd00bef5.png", vipLevel:"03", nameLock: "Send images in Chat", isLucked: true, content: `Send your favorite memes in chat, show everyone  what you mean rather than saying.`},
    {id:5, icon: "https://static.nanogames.io/assets/rakeback.459272ac.png", vipLevel:"03", nameLock: "Rakeback", isLucked: true, content: `Receive up to 20% back on house commission for every bet you make, win or lose!`},
    {id:6, icon: "https://static.nanogames.io/assets/jbfree.9634524a.png", vipLevel:"03", nameLock: "No-fee Withdrawals", isLucked: true, content: `A perk unique to NANOGAMES.IO, exchange CUB for a fee-free withdrawal every day!`},
    {id:7, icon: "https://static.nanogames.io/assets/recharge.0f6e68e9.png", vipLevel:"03", nameLock: "Recharge", isLucked: true, content: `Need a balance boost? Claim free cash back as soon as every 10 minutes.`},
    {id:8, icon: "https://static.nanogames.io/assets/chat.f51f666d.png", vipLevel:"03", nameLock: "Private chat", isLucked: true, content: `Send messages and chat with your closest friends in private on-site`},
]


</script>

<div id="mobile-screen">
    <div class="sc-hUplSX jzbUmw">
        <div class="sc-cfJLRR gQxvnl vip-top-banner">
            <div class="banner-head">
                <img class="vip-bc-img" alt="banner.png" src="https://static.nanogames.io/assets/bg_m.876e8177.png">
                <div class="vip-desc">
                    <div class="vip-club-tit">VIP - <br>Exclusive Player Benefits</div>
                    <div class="vip-club-desc">DOTPLAYPLAY invites you to join our VIP club where there is abundance of gifts, giveaways, higher cash back and unique features. Don't miss out on all the exciting and amazing fun!</div>
                </div>
            </div>
        </div>

        <div class="center-cont">
            <div class="svip-title">VIP &amp; SVIP Unlocked Rights</div>
            <div class="sc-bLdqUH bxRPMC l-box-wrap">
                <div class="sc-emDsmM Ybvgo mobile-swiper-wrap">
                    {#each vip as bb}
                    <div class="flag-wrap open">
                        <div class="top">
                            <div class="top-lock">{ bb.isLucked ? `Unlocked` : "" }</div>
                            <div class="tag-img" style="background-image: url(&quot;data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEgAAABICAYAAABV7bNHAAAAAXNSR0IArs4c6QAAAERlWElmTU0AKgAAAAgAAYdpAAQAAAABAAAAGgAAAAAAA6ABAAMAAAABAAEAAKACAAQAAAABAAAASKADAAQAAAABAAAASAAAAACQMUbvAAADBUlEQVR4Ae3b6WoTURgG4O87E+9G64YbKqK4oM1SFCRL/zVpLmMml5Gl/9IkIEq2Ki5YRMUNd+/GzDmeRMFQ07zNZK39BgLTeefMnPP0zXT+lPPluiHZdhVQuyYS9AQECBRBgAQICIBYGiRAQADE0iABAgIglgYJEBAAsTRIgIAAiKVBAgQEQCwNEiAgAGJpkAABARBLgwQICIBYGiRAQADE0iABAgIglgYJEBAAsTRIgIAAiKVBAgQEQCwNEiAgAGJpkAABARBLgwQICIBYGiRAQADE0iABAgIglgYJEBAAsTRIgIAAiKVBAgQEQCwNEiAgAGJpkAABARBLgwQICIB40Rqk7Xy7n4XZFgKImQ0x32Ollrqf3n732AJsoXnOoQdj6L5ynFw6Hv7RN5e7pVr7sO74LjHdMcZwXzbTXZ7H/833YMg8MOZQLru6/H3YivPlrSPMP10ivj0PqJkC/WlMnRV5mWTs2zCYnVmx0lgymjzbqJVZQs0EqAtjyDRCjuOtxSNfdy5+lJ83aq2jHd/3mDg2C6ipA1mcBlHIW08tfxkFAp1b2Nw6RtTxLFIMnTtOPjUg+xtuKoe8dCL2eZwJorGlauO49smzDY2ic4PkEweyjWkbR7nZeORTkAkFHZOvtU6wr3O2UeGg1xg0boJAvKXYcTOp8MdBN5rVseJm+6Q2fo7ILE/inmMDMdNDcpS3Ho9+mMSEJnWNQq15inxtn1F0a5xrBgayX6VHipSXTkXejzOBaY8tbbZOa+pCmZtB7jUykG3MY6PIzSZW3gW54bzG5Kv1M6zJPqPoxihzGAXoiQopNxOPvh3lBot2brHWPKs72j6j6Ppe5gaB7FfpqcPKXUtG3uzlgvvlnI1K65xven/1rg2b865AFuaZMvY9ZjX2etgF9ntWKjfOa7bvUcZcHbSWf4AszHNjG5NNRl4NGvC/HstXWhf4d6Ou9K/xLxDztlL2PSYRftl/wkHbL1bbF7W271HGXO6unQvl+jYp+x6TjL44aBjD1luoNC+R1t4vV6P3BL5hyhAAAAAASUVORK5CYII=&quot;); color: rgb(245, 246, 247);">
                                <span>V{bb.vipLevel}</span>
                            </div>
                        </div>
                        <div class="flag-img-wrap">
                            <img class="flag-img" src={bb.icon} alt="">
                        </div>
                        <div class="flag-box">
                            <div class="flag-tit">{bb.nameLock}</div>
                            <div class="flag-desc">{bb.content}</div>
                        </div>
                    </div>
                    {/each}
                </div>
            </div>
        </div>

                <div class="bot-other">
                    <div class="svip-title">Exclusive VIP &amp; SVIP Benefits</div>
                    <div class="card-wrap">
                        <div class="card">
                            <div class="card-cont">
                                <div class="card-img-wrap">
                                    <img class="card-img" src="https://static.nanogames.io/assets/emoji_m.ae3b136b.png" alt="">
                                </div>
                                <div class="card-box box-p-bg">
                                    <div class="card-title">Unique VIP Transfer Program</div>
                                    <div class="card-desc">DOTPLAYPLAY respects and welcomes every distinguished VIP and will give you an exclusive VIP status that you
                                        can continue your honor here. Contact us for details.</div>
                                </div>
                            </div>
                        </div>
                        <div class="card">
                            <div class="card-cont">
                                <div class="card-img-wrap">
                                    <img class="card-img" src="https://static.nanogames.io/assets/wallet_m.747f1dcc.png" alt="">
                                </div>
                                <div class="card-box ">
                                    <div class="card-title">Exclusive VIP Host</div>
                                    <div class="card-desc">There will be exclusive host for every VIP. Feel free to contact them any time.</div>
                                </div>
                            </div>
                        </div>
                        <div class="card">
                            <div class="card-cont">
                                <div class="card-img-wrap">
                                    <img class="card-img" src="https://static.nanogames.io/assets/start_m.7bbee082.png" alt="">
                                </div>
                                <div class="card-box box-p-bg">
                                    <div class="card-title">The SVIP Code</div>
                                    <div class="card-desc">Only SVIP can get code from exclusive host. Become an SVIP, rock like a superstar and have the
                                        spotlight shining on you!</div>
                                </div>
                            </div>
                        </div>
                        <div class="card">
                            <div class="card-cont">
                                <div class="card-img-wrap">
                                    <img class="card-img" src="https://static.nanogames.io/assets/gift_m.70fbc611.png" alt="">
                                </div>
                                <div class="card-box ">
                                    <div class="card-title">Secret Treasure</div>
                                    <div class="card-desc">VIP needs more Surprises in life. The higher your rank, the more surprising your secret treasure
                                        will be!</div>
                                </div>
                            </div>
                        </div>
                        <div class="card">
                            <div class="card-cont">
                                <div class="card-img-wrap">
                                    <img class="card-img" src="https://static.nanogames.io/assets/card_m.739fb4c2.png" alt="">
                                </div>
                                <div class="card-box box-p-bg">
                                    <div class="card-title">Free Coins Every Day</div>
                                    <div class="card-desc">NANOGAMES.IO offers many ways to get free coins to all our players. As a VIP you are entitled to an ever growing percentage boost of free coins.</div>
                                </div>
                            </div>
                        </div>
                        <div class="card">
                            <div class="card-cont">
                                <div class="card-img-wrap">
                                    <img class="card-img" src="https://static.nanogames.io/assets/diamond_m.6fd4401f.png" alt="">
                                </div>
                                <div class="card-box ">
                                    <div class="card-title">SVIP's Genie In A Bottle</div>
                                    <div class="card-desc">We’re rolling out the red carpet for you! Your SVIP Manager is now your private Genie ready to grant your wishes. Within reason, of course.</div>
                                </div>
                            </div>
                        </div>
                        <div class="card">
                            <div class="card-cont">
                                <div class="card-img-wrap">
                                    <img class="card-img" src="https://static.nanogames.io/assets/ship_m.73308b08.png" alt="">
                                </div>
                                <div class="card-box box-p-bg">
                                    <div class="card-title">SVIP Trip</div>
                                    <div class="card-desc">SVIP Secret Treasures will fullfill your wildest dreams. You can receive exciting all-expense-paid trips to the most exotic and entertainment filled locations on the planet. Or maybe even something better.</div>
                                </div>
                            </div>
                        </div>
                        <div class="card">
                            <div class="card-cont">
                                <div class="card-img-wrap">
                                    <img class="card-img" src="https://static.nanogames.io/assets/sail_m.bcb3baae.png" alt="">
                                </div>
                                <div class="card-box ">
                                    <div class="card-title">SVIP Life Is Suite</div>
                                    <div class="card-desc">Casinos have the most elegant hotel suites in the world. Indulge yourself with a full week of celebrity treatment including spas, room service, shows and jacuzzis. On us.</div>
                                </div>
                            </div>
                        </div>
                        <div class="card">
                            <div class="card-cont">
                                <div class="card-img-wrap">
                                    <img class="card-img" src="https://static.nanogames.io/assets/air_m.f1789377.png" alt="">
                                </div>
                                <div class="card-box box-p-bg">
                                    <div class="card-title">SVIP Party</div>
                                    <div class="card-desc">SVIP members will be chosen every year to attend our SVIP Annual Party where you will be treated as the celebrity you are! Get ready for champagne, fine dining and red carpets!</div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="foot-desc">
                    <div>Some features and benefits require specific conditions to be met. Please ask your VIP host for details</div>
                    <div>Each one of you is important to us. Whether you are here to take the bankroll or just passing some time chatting with friends.</div>
                    <div>- You all are NANOGAMES.IO. We wouldn't be here without you! -</div>
                </div>
            </div>
</div>
