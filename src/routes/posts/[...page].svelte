<script context="module">
  export const prerender = true

  /**
   * @type {import("@sveltejs/kit").Load}
   */
  export const load = async ({ fetch, params }) => {
    let page = 1
    let limit = 10

    if (params.page) {
      try {
        // a url of /posts/page/2 will come through as 'page/2' for params.page
        page = parseInt(params.page.split('page/').pop())
      } catch (e) {
        console.error(e)
      }
    }

    const fetchPostsParams = new URLSearchParams()

    fetchPostsParams.set('page', page)
    fetchPostsParams.set('limit', limit)

    const posts = await fetch(`/posts?${fetchPostsParams.toString()}`).then((res) =>
      res.json()
    )

    // if page doesn't exist, direct to page 1
    if (posts.length == 0 && page > 1) {
      return {
        redirect: `/posts`,
        status: 302
      }
    }

    return {
      props: {
        posts,
        page,
        limit
      }
    }
  }
</script>

<script>
  import ArrowLeftIcon from '$lib/components/ArrowLeftIcon.svelte'

  import ButtonLink from '$lib/components/ButtonLink.svelte'

  import PostPreview from '$lib/components/PostPreview.svelte'
  import { name } from '$lib/info.js'

  export let posts
  export let page

  $: isFirstPage = page === 1
  $: hasNextPage = posts[posts.length - 1]?.previous
</script>

<svelte:head>
  <title>{name} | Posts</title>
</svelte:head>

<p class="text-center p-8 text-2xl text-slate-300 dark:text-slate-700">Select a post to read</p>


