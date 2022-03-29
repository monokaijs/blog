<script context="module">
  /**
   * @type {import('@sveltejs/kit').Load}
   */
  export async function load({ params, fetch }) {
    const { slug } = params

    // fetch posts from endpoint so that it includes all metadata (see posts.js for explanation)
    const posts = await fetch('/posts').then((res) => res.json())
    const post = posts.find((post) => slug === post.slug)

    if (!post) {
      return {
        status: 404,
        error: 'Post not found'
      }
    }

    const component = post.isIndexFile
      ? // vite requires relative paths and explicit file extensions for dynamic imports
        await import(`../../../posts/${post.slug}/index.md`)
      : await import(`../../../posts/${post.slug}.md`)

    return {
      props: {
        ...post,
        component: component.default,
        recentPosts: await fetch('/posts?limit=2').then((res) => res.json())
      }
    }
  }

  export const prerender = true;
</script>

<script>
  import { format, parseISO } from 'date-fns'
  import { page } from '$app/stores'
  import ButtonLink from '$lib/components/ButtonLink.svelte'
  import { name, website } from '$lib/info'
  import ToC from '$lib/components/ToC.svelte'
  import PostPreview from '$lib/components/PostPreview.svelte'
  import ArrowLeftIcon from '$lib/components/ArrowLeftIcon.svelte'

  export let component

  // metadata
  export let title
  export let date
  export let preview
  export let readingTime
  export let slug
  export let next
  export let previous

  // generated open-graph image for sharing on social media. Visit https://og-image.vercel.app/ to see more options.
  const ogImage = `https://og-image.vercel.app/**${encodeURIComponent(
    title
  )}**?theme=light&md=1&fontSize=100px&images=https%3A%2F%2Fassets.vercel.com%2Fimage%2Fupload%2Ffront%2Fassets%2Fdesign%2Fhyper-color-logo.svg`

  const url = `${website}/${slug}`
</script>

<svelte:head>
  <title>{title}</title>
  <meta name="description" content={preview.text} />
  <meta name="author" content={name} />

  <!-- Facebook Meta Tags -->
  <meta property="og:url" content={url} />
  <meta property="og:type" content="website" />
  <meta property="og:title" content={title} />
  <meta property="og:description" content={preview.text} />
  <meta property="og:image" content={ogImage} />

  <!-- Twitter Meta Tags -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta property="twitter:domain" content={website} />
  <meta property="twitter:url" content={url} />
  <meta name="twitter:title" content={title} />
  <meta name="twitter:description" content={preview.text} />
  <meta name="twitter:image" content={ogImage} />
</svelte:head>
<div class="overflow-y-auto h-screen w-full">
  <article class="px-6 py-20 w-full mx-auto prose lg:prose-lg h-fit dark:prose-invert prose-img:mx-auto">

    <h1 class="!mb-2">{title}</h1>
    <p class="text-sm text-slate-500 !mb-8">
      {date}
    </p>
    <!-- <img class="rounded max-w-full mx-auto mb-4" src="{{ . }}" alt="{{ $title }}" /> -->

    <svelte:component this={component} />
  </article>
</div>