<script>
  import '../app.css'
  import '../prism.css'
  import 'focus-visible'
  import MoonIcon from 'heroicons-svelte/solid/MoonIcon.svelte'
  import SunIcon from 'heroicons-svelte/solid/SunIcon.svelte'
  import { browser } from '$app/env'
  import { name } from '$lib/info'
  import Sidebar from "$lib/components/Sidebar.svelte";
import { onMount } from 'svelte';

  let prefersLight = browser ? Boolean(JSON.parse(localStorage.getItem('prefersLight'))) : false;
  // on
</script>


<svelte:head>
  <meta charset="utf-8" />

  <meta name="viewport" content="width=device-width, initial-scale=1" />

  <title>
    Edward Nguyen :: Space
  </title>

  <meta name="description" content="Edward Nguyen's Space" />
  <meta name="author" content="MonokaiJs" />

  <link rel="stylesheet" href="/css/main.css"/>
    <link
      rel="stylesheet"
      href="https://cdn.jsdelivr.net/npm/katex@0.10.0-rc.1/dist/katex.min.css"
      integrity="sha384-D+9gmBxUQogRLqvARvNLmA9hS2x//eK1FhVb9PiU86gmcrBrJAQT8okdJ4LMp2uv"
      crossorigin="anonymous"
    />
    <script defer
      src="https://cdn.jsdelivr.net/npm/katex@0.10.0-rc.1/dist/katex.min.js"
      integrity="sha384-483A6DwYfKeDa0Q52fJmxFXkcPCFfnXMoXblOkJ4JcA8zATN6Tm78UNL72AKk+0O"
      crossorigin="anonymous"
    ></script>
</svelte:head>


<Sidebar/>
<div class="flex-1">
  <slot/>
</div>