<script>
  import { goto } from "$app/navigation";
  import AiFillEye from "svelte-icons-pack/ai/AiFillEye";
  import Icon from "svelte-icons-pack/Icon.svelte";
  import IoCloseSharp from "svelte-icons-pack/io/IoCloseSharp";
  import RiSystemArrowRightSLine from "svelte-icons-pack/ri/RiSystemArrowRightSLine";
  import { handleLogin } from "$lib/firebaseAuth/index";
  import {
    handleGoogleAuth,
    handleFacebookAuth,
  } from "$lib/firebaseAuth/index";
  import { createEventDispatcher } from "svelte";
  import { browser } from "$app/environment";
  import { onMount } from "svelte";
  import { current_route } from "$lib/store/routes";
  import { error_msgS, is_loadingS } from "$lib/nestedpages/auth/signup/store";
  import Forget from "../forget/+page.svelte";
  import { isLightMode } from "../../../lib/store/theme";
  import { screen } from "$lib/store/screen"
  const dispatch = createEventDispatcher();
  let email = "";
  let password = "";
  const googleAuth = () => {
    handleGoogleAuth();
  };

  const handleFacebookAuthi = () => {
    handleFacebookAuth();
  };

  const handleSubmit = () => {
    if (!email) {
      error_msgS.set("email field can't be empty");
      setTimeout(() => {
        error_msgS.set(false);
      }, 4000);
    } else if (!password) {
      error_msgS.set("Password is required");
      setTimeout(() => {
        error_msgS.set(false);
      }, 4000);
    } else {
      handleLogin(email, password);
    }
  };

  const handleCancel = () => {
    // dispatch("close", 3)
    goto("/");
  };

  let is_mobile = false;
  onMount(() => {
    if (browser && window.innerWidth < 650) {
      is_mobile = true;
    } else {
      is_mobile = false;
    }
  });

  // $:{
  //     const currentPath = browser && window.location.pathname;
  //     if(currentPath === "/forget"){
  //         is_forget_password = true
  //     }else if( currentPath === "/login"){
  //         is_forget_password = false
  //     }
  // }

  let is_forget_password = false;
  const handleForgetPassword = () => {
    const currentPath = browser && window.location.pathname;
    if (currentPath === "/forget") {
      window.history.replaceState(null, "", $current_route);
      is_forget_password = false;
    } else {
      current_route.set(currentPath);
      is_forget_password = true;
      window.history.replaceState(null, "forget", "/forget");
    }
  };
</script>

<div class="sc-bkkeKt kBjSXI">
  {#if $error_msgS}
    <div class="error-message">
      <div class="hTTvsjh">
        <div>{$error_msgS}</div>
      </div>
    </div>
  {/if}

  <div
    class="dialog"
    style={`${
    $screen < 650
        ? "transform: scale(1) translateZ(5px);"
        : "opacity: 1; width: 464px; height: 631px; margin-top: -315.5px; margin-left: -232px;"
    }  `}
  >
    <div class="dialog-head has-close">
      <img
        alt="logo"
        class="sc-bOtlzW QccSQ"
        src="https://res.cloudinary.com/dxwhz3r81/image/upload/v1697848521/dpp-logowhite_lbifm7.png"
      />
    </div>

    <button
      on:click={() => handleCancel()}
      class="sc-ieecCq fLASqZ close-icon dialog-close"
    >
      <Icon
        src={IoCloseSharp}
        size="18"
        color="rgb(255, 255, 255)"
        className="custom-icon"
        title="arror"
      />
    </button>

    {#if !is_forget_password}
      <div
        class="dialog-body no-style sc-zjkyB ipnwmW"
        style="z-index: 2; transform: none;"
      >
        <div class="welcome">
          <div class="msg1">BUILD THE BEST CRYPTO CASINO TOGETHER</div>
          <img
            src="https://res.cloudinary.com/dxwhz3r81/image/upload/v1704543204/NIKE1_34_1_ji6ln1.png"
            alt=""
          />
        </div>
        <div
          class={$isLightMode ? "light-bg sc-dkPtRN jScFby scroll-view hide-bar sc-bjztik ceTZhf" :"sc-dkPtRN jScFby scroll-view hide-bar sc-bjztik ceTZhf"}
          style="transform: none;"
        >
          <div id="login" 
          class={$isLightMode ? "light-bg sc-czvZiG lnrkkr" :"sc-czvZiG lnrkkr"}>
            <div class="box">
              <div class="sc-ezbkAF kDuLvp input">
                <div class="input-label">Email Address</div>
                <div class={$isLightMode ? "light-input-control input-control": "input-control"}>
                  <input
                    bind:value={email}
                    type="text"
                    autocomplete="off"
                    placeholder="Email"
                  />
                </div>
              </div>
              <div class="sc-ezbkAF kDuLvp input sc-bYoBSM ixxYMF">
                <div class="input-label">
                  <div style="flex: 1 1 0%;">Login Password</div>
                  <button on:click={handleForgetPassword}
                    >Forgot password?</button
                  >
                </div>
                <div class={$isLightMode ? "light-input-control input-control": "input-control"}>
                  <input
                    bind:value={password}
                    type="password"
                    autocomplete="off"
                    placeholder="Login Password"
                  />
                  <svg
                    xmlns:xlink="http://www.w3.org/1999/xlink"
                    class="sc-gsDKAQ hxODWG icon"
                  >
                    <use xlink:href="#icon_View"></use>
                  </svg>
                </div>
              </div>
            </div>
            <hr />
            <div class="buttons">
              <button
                disabled={$is_loadingS}
                type="submit"
                on:click={handleSubmit}
                class="sc-iqseJM sc-bqiRlB cBmlor eWZHfu button button-big"
              >
                <div class="button-inner">
                  {#if $is_loadingS}
                    <div class="center">
                      <div class="wave"></div>
                      <div class="wave"></div>
                      <div class="wave"></div>
                      <div class="wave"></div>
                      <div class="wave"></div>
                      <div class="wave"></div>
                      <div class="wave"></div>
                      <div class="wave"></div>
                      <div class="wave"></div>
                      <div class="wave"></div>
                    </div>
                  {:else}
                    Sign in
                  {/if}
                </div>
              </button>
              <button
                on:click={() => goto("/register")}
                class="sc-iqseJM sc-crHmcD cBmlor gEBngo button button-big signup"
              >
                <div class="button-inner">
                  <span>Sign up</span>
                  <Icon
                    src={RiSystemArrowRightSLine}
                    size="18"
                    color=" rgb(245, 246, 247)"
                    className="sc-gsDKAQ hxODWG icon"
                    title="arror"
                  />
                </div>
              </button>
            </div>
          </div>

          <div id="other-login" class="sc-jFkwbb iajVfs">
            <div class="box-title">Log in directly with</div>
            <div class="other-group">
              <button
                on:click={googleAuth}
                id="gg_login"
                type="button"
                title="google"
              >
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32">
                  <path fill="#fa455e" d="M16 0a16 16 0 110 32 16 16 0 010-32z"
                  ></path>
                  <path
                    fill="#fff"
                    d="M19.5 12.3c-.5-.5-1.1-.9-1.8-1a4.8 4.8 0 00-2-.2c-.9 0-1.7.4-2.3 1a5 5 0 00-2 4 5 5 0 004 4.8 5 5 0 001.6 0c.8 0 1.6-.3 2.2-.7.5-.4 1-.9 1.2-1.4l.3-.9v-.2h-4.4v-3.2h7.5l.2.1.1 1v1.2c0 .5 0 1-.2 1.6v-.1a7.4 7.4 0 01-1.4 3 7 7 0 01-3 2.4h-.1c-.6.2-1.2.4-1.9.4a8.8 8.8 0 01-1.9 0c-.8 0-1.5-.1-2.2-.4-.9-.4-1.6-.8-2.3-1.4-1-.8-1.9-2-2.4-3.2l-.5-1.9v-1.4-.1c0-.9.2-1.7.4-2.5.3-.7.7-1.4 1.2-2 1-1.4 2.5-2.5 4.3-3l1.5-.3a11.1 11.1 0 011.3 0 7.7 7.7 0 014.8 2l-.1.3-2 2h-.1z"
                  ></path>
                </svg>
              </button>

              <button
                on:click={handleFacebookAuthi}
                id="fb_login"
                type="button"
                title="facebook"
              >
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32">
                  <path
                    fill="#fff"
                    d="M31.7 16.3a15.7 15.7 0 11-31.4 0 15.7 15.7 0 0131.4 0z"
                  ></path>
                  <path
                    fill="#227aee"
                    d="M0 16a16 16 0 0013.4 15.8V20.6h-4v-4.7h4v-4.4c0-2.7 2.3-5.7 6.5-5.6 1.5 0 3.4.5 3.4.5v4s-1.9-.2-3 0c-1.6.2-2 1.4-2 2v3.3h4.9l-1 4.9h-3.8v11.2A16 16 0 100 16z"
                  ></path>
                </svg>
              </button>
              <div class="line"></div>
            </div>
          </div>
        </div>
      </div>
    {:else}
      <Forget on:close={handleForgetPassword} on:cancel={handleCancel} />
    {/if}
  </div>
</div>

<style>

  .light-input-control{
    border: 1px solid rgb(233, 234, 242) !important;
    background-color: rgb(245, 246, 250) !important;
  }
  .kBjSXI {
    position: fixed;
    z-index: 1000;
    inset: 0px;
    background-color: rgb(0, 0, 0);
    filter: none !important;
  }

  .ipnwmW {
    background-color: #1C8B00;
  }

  .dialog {
    position: absolute;
    display: flex;
    flex-direction: column;
    left: 50%;
    top: 50%;
    width: 464px;
    height: 720px;
    margin: -375px 0px 0px -280px;
    transition-property: width, height, margin-left, margin-top;
    transition-duration: 0.5s;
    border-radius: 1.25rem;
    overflow: hidden;
    /* background-color: rgb(23, 24, 27); */
  }

  .dialog-head.has-close {
    margin-right: 3.75rem;
  }

  .dialog-head {
    position: relative;
    z-index: 10;
    flex: 0 0 auto;
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    height: 3.75rem;
    margin-left: 1.125rem;
    transition: all 0.5s ease 0s;
  }

  img {
    overflow-clip-margin: content-box;
    overflow: clip;
  }


  .ipnwmW.dialog-body {
    padding: 0px;
  }

  .dialog-body {
    position: absolute;
    inset: 0px;
    display: flex;
    overflow: hidden;
  }

  .ipnwmW .welcome {
    height: 11.875rem;
    position: absolute;
    top: 3.75rem;
    left: 1.25rem;
    right: 0.3125rem;
    z-index: 1;
    color: rgb(245, 246, 247);
  }

  .dialog-body > div {
    flex: 1 1 0%;
  }

  .ipnwmW .welcome .msg1 {
    font-size: 1.5rem;
    font-weight: bold;
    width: 14.375rem;
    line-height: 1.2;
    margin-top: 1.25rem;
  }

  .ipnwmW .welcome img {
    height: 13.75rem;
    position: absolute;
    right: 0px;
    top: -1.875rem;
  }

  .dialog-body > div {
    flex: 1 1 0%;
  }

  .ipnwmW #login {
    padding-top: 0px;
  }

  .lnrkkr .box {
    padding: 1.5rem 1.25rem;
  }

  .lnrkkr .box > .input:first-of-type {
    margin-top: 0.25rem;
  }

  .kDuLvp {
    margin-top: 1rem;
  }

  .kDuLvp .input-label {
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    line-height: 1em;
    height: 1.25rem;
    margin: 0px 0.75rem 0.375rem;
    color: rgba(153, 164, 176, 0.6);
  }

  .ipnwmW #login {
    padding-top: 0px;
  }

  .lnrkkr {
    background-color: rgb(30, 32, 36);
  }

  .lnrkkr .buttons {
    padding: 1.25rem 2.5rem;
    display: flex;
  }

  .iajVfs .box-title {
    text-align: center;
    width: 100%;
    line-height: 1;
    margin-bottom: 0.875rem;
    color: rgba(153, 164, 176, 0.6);
  }

  .iajVfs {
    padding: 1rem 2.5rem 1.25rem;
    display: flex;
    flex-direction: column;
    -webkit-box-align: center;
    align-items: center;
  }

  .iajVfs .box-title {
    text-align: center;
    width: 100%;
    line-height: 1;
    margin-bottom: 0.875rem;
    color: rgba(153, 164, 176, 0.6);
  }

  .iajVfs .other-group {
    border-radius: 1.75rem;
    background-color: rgba(49, 52, 60, 0.5);
    display: flex;
    -webkit-box-pack: justify;
    justify-content: space-between;
  }

  .iajVfs .other-group button {
    display: flex;
    height: 3.5rem;
    width: 3.5rem;
    -webkit-box-align: center;
    align-items: center;
    -webkit-box-pack: center;
    justify-content: center;
    overflow: hidden;
    position: relative;
  }

  .dialog-body > div {
    flex: 1 1 0%;
  }

  .ceTZhf {
    position: absolute;
    inset: 16.25rem 0px 0px;
    height: auto;
    border-top-left-radius: 1.25rem;
    border-top-right-radius: 1.25rem;
    background-color: rgb(23, 24, 27);
  }

  .jScFby {
    box-sizing: border-box;
    height: 100%;
    overflow-y: auto;
    touch-action: pan-y;
    overscroll-behavior: contain;
  }

  .QccSQ {
    height: 1.7rem;
    margin: 2rem 10px;
  }

  .iajVfs .other-group button {
    display: flex;
    height: 3.5rem;
    width: 3.5rem;
    -webkit-box-align: center;
    align-items: center;
    -webkit-box-pack: center;
    justify-content: center;
    overflow: hidden;
    position: relative;
  }

  .iajVfs .other-group svg {
    width: 2.25rem;
    height: 2.25rem;
  }

  .lnrkkr hr {
    height: 1px;
    margin: 0px;
    border: none;
    background-color: rgba(62, 72, 79, 0.3);
  }

  .lnrkkr .buttons {
    padding: 1.25rem 2.5rem;
    display: flex;
  }

  .lnrkkr .buttons .button:first-of-type {
    flex: 0 0 auto;
    margin-right: 0.625rem;
  }

  .cBmlor > .button-inner {
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    -webkit-box-pack: center;
    justify-content: center;
    width: 100%;
    height: 100%;
  }

  .cBmlor.button-big {
    height: 3.625rem;
  }

  .cBmlor.button-big {
    height: 3.625rem;
  }

  .lnrkkr .signup {
    color: rgb(245, 246, 247);
    background-color: rgb(49, 52, 60);
  }

  .lnrkkr .button {
    flex: 1 1 0%;
  }

  .gEBngo.button {
    box-shadow: rgba(29, 34, 37, 0.1) 0px 4px 8px 0px;
    background-color: rgb(107, 113, 128);
  }

  .jScFby {
    box-sizing: border-box;
    height: 100%;
    overflow-y: auto;
    touch-action: pan-y;
    overscroll-behavior: contain;
  }

  .ceTZhf {
    position: absolute;
    inset: 16.25rem 0px 0px;
    height: auto;
    border-top-left-radius: 1.25rem;
    border-top-right-radius: 1.25rem;
    background-color: rgb(23, 24, 27);
  }

  .kDuLvp .input-control input {
    flex: 1 1 0%;
    width: 100%;
    height: 100%;
    min-width: 1rem;
    padding: 0px;
    border: none;
    outline: none;
    background-color: transparent;
    color: rgb(245, 246, 247);
  }

  input:-webkit-autofill {
    -webkit-box-shadow: 200px 200px 100px #273642 inset;
    box-shadow: 200px 200px 100px #273642 inset;
    -webkit-text-fill-color: var(--autofill-color);
  }

  .icon {
    width: 1rem;
    height: 1rem;
    margin-left: 0.375rem;
    opacity: 0.6;
    fill: rgb(245, 246, 247);
  }

  /* ============================= mobile ===================================== */

  .kBjSXI {
    position: fixed;
    z-index: 1000;
    inset: 0px;
    background-color: rgba(0, 0, 0, 0.507);
    filter: none !important;
  }

  .dialog {
    position: absolute;
    display: flex;
    flex-direction: column;
    left: 50%;
    top: 50%;
    width: 464px;
    height: 720px;
    margin: -375px 0px 0px -280px;
    transition-property: width, height, margin-left, margin-top;
    transition-duration: 0.5s;
    border-radius: 1.25rem;
    overflow: hidden;
    background-color: rgb(23, 24, 27);
  }

  .dialog-head.has-close {
    margin-right: 3.75rem;
  }
  .dialog-head {
    position: relative;
    z-index: 10;
    flex: 0 0 auto;
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    height: 3.75rem;
    margin-left: 1.125rem;
    transition: all 0.5s ease 0s;
  }
  .fLASqZ {
    position: absolute;
    right: 0px;
    top: 0px;
    z-index: 11;
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    -webkit-box-pack: center;
    justify-content: center;
    width: 3.75rem;
    height: 3.75rem;
    cursor: pointer;
  }

  .dialog-body > div {
    flex: 1 1 0%;
  }
  .dA-dCPD .welcome .msg1 {
    font-size: 1.5rem;
    font-weight: bold;
    width: 14.375rem;
    line-height: 1.2;
    margin-top: 1.25rem;
  }
  .dA-dCPD .welcome img {
    height: 12.75rem;
    position: absolute;
    right: 0px;
    top: -1.875rem;
  }
  .dialog-body > div {
    flex: 1 1 0%;
  }

  .kDuLvp .input-label {
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    line-height: 1em;
    height: 1.25rem;
    margin: 0px 0.75rem 0.375rem;
    color: rgba(153, 164, 176, 0.6);
    font-size: 12px;
  }

  .kDuLvp .input-control {
    position: relative;
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    border-radius: 1.25rem;
    border: 1px solid rgb(45, 48, 53);
    background-color: rgba(45, 48, 53, 0.5);
    height: 3.5rem;
    padding: 0px 1.25rem;
    opacity: 1;
  }
  .kDuLvp .input-control input {
    flex: 1 1 0%;
    width: 100%;
    height: 100%;
    min-width: 1rem;
    padding: 0px;
    border: none;
    background-color: transparent;
    color: rgb(245, 246, 247);
    outline: none;
  }

  .cBmlor {
    display: block;
    width: 100%;
    border-radius: 6.25rem;
    height: 3rem;
    font-weight: bold;
    cursor: pointer;
    transition: transform 0.2s cubic-bezier(0.36, 0.66, 0.04, 1) 0s;
  }
  .cBmlor.button-big {
    height: 3.625rem;
  }

  .jBwyNM .buttons .button:first-of-type {
    width: 11rem;
    flex: 0 0 auto;
    margin-right: 0.625rem;
  }

  .cBmlor > .button-inner {
    display: flex;
    -webkit-box-align: center;
    align-items: center;
    -webkit-box-pack: center;
    justify-content: center;
    width: 100%;
    height: 100%;
  }

  @media screen and (min-width: 650px) {
    .lnrkkr .buttons .button-big {
      width: 15rem;
    }
  }

  @media screen and (max-width: 650px) {
    .dialog {
      width: 100%;
      height: 100%;
      left: 0px;
      top: 0px;
      margin: 0px;
      border-radius: 0px;
    }
    .lnrkkr .buttons .button-big {
      width: 12rem;
    }

    *,
    *:before,
    *:after {
      box-sizing: border-box;
    }
    img {
      overflow-clip-margin: content-box;
      overflow: clip;
    }
  }

  .gIMEzD .other-group button {
    display: flex;
    height: 3.5rem;
    width: 3.5rem;
    -webkit-box-align: center;
    align-items: center;
    -webkit-box-pack: center;
    justify-content: center;
    overflow: hidden;
    position: relative;
  }
  .gIMEzD .other-group svg {
    width: 2.25rem;
    height: 2.25rem;
  }
</style>
