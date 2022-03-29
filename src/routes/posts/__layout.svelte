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

    const posts = await fetch(`/posts.json?${fetchPostsParams.toString()}`).then((res) =>
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

<div class="flex h-screen relative">

  <section
    class="w-full h-full md:min-w-[400px] md:w-1/4 bg-slate-50 dark:bg-slate-800 border-r border-slate-200 dark:border-slate-700 flex flex-col py-3 overflow-y-auto scroll-area">
    <a href="/posts">
      <h2 class="font-bold mb-5 py-1 pl-12 pr-3 md:px-3">Posts</h2>
    </a>
    <div class="space-y-2.5">
      {#each posts as post}
        <a class="block px-3 py-4 hover:bg-slate-200 dark:hover:bg-slate-700" href={`/posts/${post.slug}`}>
          <h3 class="text-lg font-semibold mb-0.5">{post.title}</h3>
          <div class="text-sm text-slate-500 dark:text-slate-400 line-clamp-2">
            {@html post.preview.html}
          </div>
        </a>
      {/each}
    </div>
  </section>

  <main class="hidden md:grid h-screen place-items-center flex-1">
    <slot/>
  </main>

</div>