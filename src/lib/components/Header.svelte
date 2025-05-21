<script>
  import { base } from "$app/paths";
  import wordmark from "$lib/assets/wordmark-sticker.svg";
  import Menu from "$lib/components/Header.Menu.svelte";

  // State
  let isMenuOpen = $state(false);
  let menuRef;
  let menuButtonRef;

  // Methods
  function closeMenu(skipFocus = false) {
    isMenuOpen = false;
    menuButtonRef.removeAttribute("aria-hidden");
    if (!skipFocus) menuButtonRef.focus();
  }

  function openMenu() {
    isMenuOpen = true;
  }
</script>

<header>
  <!-- Empty space on left to balance layout -->
  <div class="desktop-nav">
    <!-- Intentionally empty for balance -->
  </div>

  <!-- Logo centered -->
  <div class="logo">
    <a href="https://vermont-complex-systems.github.io/VSCI-cool-website/" aria-label="The VCSI">
      <img src={wordmark} alt="The VCSI" />
    </a>
  </div>

  <!-- Menu buttons on right -->
  <div class="menu-button">
    <a href="{base}/about">About</a>
    <a
      href="#"
      bind:this={menuButtonRef}
      onclick={openMenu}
      aria-label="Open menu"
      aria-controls="nav-content"
      class="more-link"
    >
      More
    </a>
  </div>
</header>

<!-- Mobile menu component -->
<Menu visible={isMenuOpen} bind:this={menuRef} close={closeMenu} />

<style>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 2rem 1rem 2.5rem; /* Increased bottom padding for logo */
    max-width: var(--content-width, 1200px);
    margin: 0 auto;
    position: relative; /* For absolute positioning of logo */
  }

  .logo {
    max-width: 200px;
    transition: transform 0.25s ease;
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    z-index: 0; /* Ensure logo is behind text if they overlap */
  }

  .logo:hover {
    transform: translateX(-50%) rotate(-2deg) scale(1.05);
  }

  .logo a {
    display: block;
    border: none;
  }

  .logo img {
    width: 100%;
    height: auto;
  }

  /* Space for left and right sides */
  .desktop-nav,
  .menu-button {
    width: 25%;
    z-index: 1; /* Ensure they're above the logo */
  }
  
  /* Right align menu button */
  .menu-button {
    text-align: right;
    display: flex;
    justify-content: flex-end;
    gap: 1.5rem;
    align-items: center;
  }

  .menu-button a {
    text-decoration: none;
    color: var(--color-fg, #000);
    font-weight: 500;
    transition: transform 0.25s ease;
    display: inline-block;
  }

  .menu-button a:hover {
    transform: rotate(2deg) scale(1.05);
  }

  /* Mobile styles */
  @media (max-width: 768px) {
    header {
      padding-bottom: 1.5rem; /* Less bottom padding on mobile */
    }
    
    .desktop-nav,
    .menu-button {
      width: auto;
    }
    
    .logo {
      max-width: 150px; /* Smaller on mobile */
    }
    
    .menu-button {
      gap: 1rem;
    }
  }
</style>