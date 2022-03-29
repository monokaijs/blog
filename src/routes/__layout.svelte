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
</svelte:head>


<Sidebar/>
<div class="flex-1">
  <slot/>
</div>