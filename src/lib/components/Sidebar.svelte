<script>
  import CloseIcon from "./CloseIcon.svelte";
  import ExternalIcon from "./ExternalIcon.svelte";
  import FacebookIcon from "./FacebookIcon.svelte";
import LinkedInIcon from "./LinkedInIcon.svelte";
  import MenuIcon from "./MenuIcon.svelte";
  import NewsletterWidget from "./NewsletterWidget.svelte";
  import SunIcon from "./SunIcon.svelte";

  let showMenu = true;

  const toggleSidebar = () => {
    console.log("clicked")
    showMenu = !showMenu;
  }

</script>
<aside
  class:!translate-x-0={showMenu}
  class="will-change-transform transform transition-transform -translate-x-full absolute top-0 left-0 md:relative md:translate-x-0 w-3/4 md:w-60 h-full min-h-screen p-3 bg-slate-50 dark:bg-slate-800 border-r border-slate-200 dark:border-slate-700 flex flex-col gap-2.5 z-20 sidebar"
>
  <p class="font-bold mb-5 flex items-center gap-2">
    <button
      aria-label="Close sidebar"
      class="md:hidden menu-trigger-close p-1 rounded text-slate-800 dark:text-slate-50 hover:bg-slate-200 dark:hover:bg-slate-700"
      on:click={toggleSidebar}
    >
      <CloseIcon/>
    </button>
    <a href="/" class="px-2">
      <span>Edward Nguyen's Space.</span>
    </a>
    <button
      aria-label="Toggle dark mode"
      class="dark-mode-toggle p-2 rounded border dark:border-slate-700 hover:bg-slate-200 dark:hover:bg-slate-700">
      <SunIcon/>
    </button>
  </p>

  
  <ul class="list-none flex flex-col gap-1">
    <li>
      <a class="px-2 py-1.5 rounded-md text-sm flex items-center justify-between hover:bg-slate-200 dark:hover:bg-slate-700" href="/">
        <span>Home</span>
      </a>
    </li>
    <li>
      <a class="px-2 py-1.5 rounded-md text-sm flex items-center justify-between hover:bg-slate-200 dark:hover:bg-slate-700" href="/posts/">
        <span>Articles</span>
      </a>
    </li>
    <li>
      <a class="px-2 py-1.5 rounded-md text-sm flex items-center justify-between hover:bg-slate-200 dark:hover:bg-slate-700" href="/portfolio/">
        <span>Portfolio</span>
      </a>
    </li>
    <li>
      <a class="px-2 py-1.5 rounded-md text-sm flex items-center justify-between hover:bg-slate-200 dark:hover:bg-slate-700"
        href="/" target="_blank" rel="noopener">
        <span>MonokaiToolkit</span>
        <span>
          <ExternalIcon/>
        </span>
      </a>
    </li>
  </ul>

  <div class="flex-1"></div>

  <NewsletterWidget/>

  <ul class="list-none flex flex-wrap justify-center gap-1 pt-2 border-t border-slate-200 dark:border-slate-600">
    <li>
      <a class="px-2 py-1.5 rounded-md text-sm block text-slate-800 dark:text-slate-50 hover:bg-slate-200 dark:hover:bg-slate-700"
        href="https://www.facebook.com/monokaijssss" target="_blank" rel="noopener noreferrer">
        <span class="sr-only">Edward Nguyenzz</span>
        <span>
          <FacebookIcon width={16}/>
        </span>
      </a>
    </li>
    <li>
      <a class="px-2 py-1.5 rounded-md text-sm block text-slate-800 dark:text-slate-50 hover:bg-slate-200 dark:hover:bg-slate-700"
        href="https://www.facebook.com/monokaijssss" target="_blank" rel="noopener noreferrer">
        <span class="sr-only">Edward Nguyenzz</span>
        <span>
          <LinkedInIcon width={16}/>
        </span>
      </a>
    </li>
  </ul>
</aside>

<div
  class:hidden={!showMenu}
  class="fixed bg-slate-700 bg-opacity-5 transition duration-200 ease-in-out inset-0 z-10 pointer-events-auto md:hidden left-0 top-0 w-full h-full hidden menu-overlay"
>
</div>

<button
  aria-label="Toggle Sidebar"
  class="md:hidden absolute top-3 left-3 z-10 menu-trigger p-1 rounded text-slate-800 dark:text-slate-50 hover:bg-slate-100"
  on:click={toggleSidebar}
>
  <MenuIcon/>
</button>