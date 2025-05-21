<script>
  import { base } from "$app/paths";
  import { afterNavigate } from "$app/navigation";
  import copy from "$data/misc.json";
  import { about, follow } from "$data/links.js";
  import focusTrap from "$actions/focusTrap.js";
  
  // Props
  let { visible, close } = $props();
  
  // Element references
  let mainEl;
  let closeBtnEl;
  let slideNav;
  let active = false;
  
  // Methods
  export const open = () => {
    closeBtnEl?.focus();
    mainEl?.setAttribute("aria-hidden", true);
  };
  
  const onClose = async (e) => {
    if (e?.type === "keyup" && e?.key !== "Escape") return;
    mainEl?.removeAttribute("aria-hidden");
    visible = false;
    close(e === "skip");
  };
  
  // Setup
  $effect(() => {
    mainEl = document.querySelector("main");
  });
  
  afterNavigate(() => {
    onClose("skip");
  });
</script>

<svelte:window on:keyup={onClose} />

<nav id="nav-menu" class:visible use:focusTrap aria-hidden={!visible}>
  <div class="nav-content" class:visible class:active bind:this={slideNav}>
    <button class="btn-close" aria-label="close menu" bind:this={closeBtnEl} onclick={onClose}>
      ✕
    </button>
    
    <section class="links">
      <div class="about">
        <h4>About Us</h4>
        <ul>
          <li><a href="{base}/about">About</a></li>
        </ul>
      </div>
      
      <div class="follow">
        <h4>Follow Us</h4>
        <ul>
          {#each follow as { name, url }}
            {@const slug = name.toLowerCase().replace(/[^a-z]/g, "_")}
            <li>
              <a href={url} target="_blank" rel="noreferrer">
                <img src="{base}/assets/stickers/{slug}@2x.png" alt="{name} logo" />
                <span>{name}</span>
              </a>
            </li>
          {/each}
        </ul>
      </div>
    </section>
  </div>
</nav>

<style>
  nav {
    position: fixed;
    top: 0;
    right: 0;
    width: 100%;
    max-width: min(360px, 90vw); /* Constrain to 90% of viewport width if smaller than 360px */
    height: 100svh;
    z-index: calc(var(--z-overlay) + 1);
    background: var(--color-uvm-bg);
    color: var(--color-bg);
    visibility: hidden;
    transform: translate(100%, 0);
    transition: transform var(--transition-medium);
    overflow-y: auto; /* Allow scrolling if content is tall */
    overflow-x: hidden; /* Prevent horizontal overflow */
  }
  
  nav.visible {
    visibility: visible;
    transform: translate(0, 0);
  }
  
  h4 {
    font-family: var(--mono);
    font-size: var(--font-size-xsmall);
    text-transform: uppercase;
    -webkit-font-smoothing: antialiased;
    margin-top: 0;
  }
  
  .links {
    display: flex;
    flex-direction: column; /* Stack sections vertically on mobile */
    align-items: flex-start;
    gap: 32px;
    padding: 0 24px 24px; /* Add bottom padding */
    width: 100%;
    box-sizing: border-box;
  }
  
  .links > div {
    width: 100%;
  }
  
  .links ul {
    padding: 0;
    margin: 0;
    list-style-type: none;
    width: 100%;
  }
  
  .links li {
    font-family: var(--sans);
    padding: 0;
    margin: 0;
    margin-bottom: 12px;
    transition: transform calc(var(--1s) * 0.25);
    transform-origin: center center;
    width: 100%;
  }
  
  .links li a {
    display: flex;
    align-items: center;
    color: currentColor;
    text-decoration: none;
    width: 100%;
  }
  
  .links li a span {
    margin-left: 8px;
    border: none;
    text-decoration: none;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  
  .links li:hover img {
    transform: rotate(var(--left-tilt-double)) scale(1.05);
  }
  
  .follow img {
    width: 36px; /* Slightly smaller icons */
    height: 36px;
    object-fit: contain;
    flex-shrink: 0;
  }
  
  .follow li:hover span {
    color: var(--color-link-hover);
  }
  
  /* Larger screens - horizontal layout */
  @media (min-width: 480px) {
    .links {
      flex-direction: row;
    }
    
    .links > div {
      width: 50%;
    }
    
    .follow img {
      width: 42px;
      height: 42px;
    }
  }
  
  .btn-close {
    font-size: 1.5rem;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 42px;
    height: 42px;
    background: transparent;
    border: none;
    color: inherit;
    cursor: pointer;
    padding: 8px;
    margin: 8px 0 24px 8px; /* Positioned to the left */
  }
  
  .btn-close:hover {
    color: var(--color-uvm-fg);
  }

  /* Make sure Follow section is properly visible */
  .follow {
    display: block;
  }
</style>