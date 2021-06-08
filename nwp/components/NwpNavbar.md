---
title: Nwp-Navbar
author: https://github.com/sonjavanteese
date: Mai 17, 2021 - 21:33 
tags:
  - Svelte
  - Navbar
categories:
  - Nwp-Components
---

## Nwp-Navbar

| Prop Name | Type    | Default | Func                         |
|-----------|---------|---------|------------------------------|
| sidebar   | boolean | true    | has Sidebar                  |
| appname   | string  | Nwp-App | Brand Name                   |
| dark      | boolean | false   | set Background Color to Dark |

| Slots   |
|---------|
| default |


**Navbar.svelte**

```html
<script>
   import { isSbOpen } from '../store.js';
   export let sidebar = true;
   export let appname = "Nwp-App";
   export let dark = false;
   const togBtnOpen = `<svg width="32px" height="32px" viewBox="0 0 20 20" fill="currentColor" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M4.5 13.5A.5.5 0 015 13h10a.5.5 0 010 1H5a.5.5 0 01-.5-.5zm0-4A.5.5 0 015 9h10a.5.5 0 010 1H5a.5.5 0 01-.5-.5zm0-4A.5.5 0 015 5h10a.5.5 0 010 1H5a.5.5 0 01-.5-.5z" clip-rule="evenodd"/></svg>`;
   const togBtnClose = `<svg width="32px" height="32px" viewBox="0 0 20 20" fill="currentColor" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M5.646 5.646a.5.5 0 000 .708l8 8a.5.5 0 00.708-.708l-8-8a.5.5 0 00-.708 0z" clip-rule="evenodd"/><path fill-rule="evenodd" d="M14.354 5.646a.5.5 0 010 .708l-8 8a.5.5 0 01-.708-.708l8-8a.5.5 0 01.708 0z" clip-rule="evenodd"/></svg>`;
   const toggleSb = () => {
      if ($isSbOpen) {
         isSbOpen.set(false)
      } else {
         isSbOpen.set(true)
      }
   }
</script>

<nav class="flexbar" class:dark={dark}>
   <div class="titel">{appname}</div>
   <slot></slot>
   {#if sidebar}
   <button on:click={toggleSb} class="baritem">
      {#if $isSbOpen}
         {@html togBtnClose}
      {:else}
         {@html togBtnOpen}
      {/if}
   </button>
   {:else}
   <span class="barblank"></span>
   {/if}
</nav>

<style>
   :root {
      --navbar-body-color: #F6F6F6; 
      --navbar-body-bg: #2172D2; 
      --navbar-body-color-dark: #F6F6F6; 
      --navbar-body-bg-dark: #424656;
      --navbar-body-border: #2172D2; 
      --navbar-body-height: 50px; 
      --navbar-active-bg: rgba(204, 204, 204, 0.4);
   }  
   nav {
      background-color: var(--navbar-body-bg);
      color: var(--navbar-body-color);
   }
   nav.dark {
      background-color: var(--navbar-body-bg-dark);
      color: var(--navbar-body-color-dark);
   }
   .flexbar {
      display: flex;
      flex-wrap: nowrap;
      align-items: center;
      min-height: var(--navbar-body-height);
   }
   .flexbar > * {
      flex: 0 1 auto;
      align-self: center;
   }
   .flexbar > button {
      background-color: transparent;
      border-color: transparent;
      outline: none;
      border-radius: 0;
      cursor: pointer;
      color: var(--navbar-body-color);
   }
   .flexbar > button:active {
      background-color: var(--navbar-active-bg);
   }
   .flexbar > .titel {
      flex: 1 1 auto;
      font-size: 1.1rem;
      font-weight: 600;
      padding: 0 0.5rem;
   }
   .barblank {
      min-height: var(--navbar-body-height);
      width: 1px;  
   }
   .baritem {
      display: flex;
      flex-wrap: nowrap;
      justify-content: center;
      align-content: center;
      align-items: center;
      min-height: var(--navbar-body-height);
      min-width: var(--navbar-body-height);
   }
</style>
```
