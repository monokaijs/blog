<script context="module">
  export const prerender = true

  export const load = async ({ fetch }) => {
    return {
      props: {
        recentPosts: await fetch('/posts?limit=2').then((res) => res.json())
      }
    }
  }
</script>

<script>
  import ButtonLink from '$lib/components/ButtonLink.svelte'
  import FacebookIcon from '$lib/components/FacebookIcon.svelte';
  import LinkedInIcon from '$lib/components/LinkedInIcon.svelte';
  import PostPreview from '$lib/components/PostPreview.svelte'
  import { name } from '$lib/info.js';
</script>

<svelte:head>
  <title>{name}</title>
</svelte:head>

<main class="h-screen overflow-y-auto">
  <div class="px-6 py-20 w-full lg:w-[580px] mx-auto prose dark:prose-invert h-fit prose-img:mx-auto">
    <div class="flex flex-col flex-grow">
      <div class="intro">
        <div class="flex flex-row align-middle items-center">
          <div class="avatar-container mr-4">
            <img class="avatar w-10" src="https://i.imgur.com/89LuXnr.jpg" alt="avatar"/>
          </div>
          <span class="text-dark-900 dark:text-light-600">
            <b>Edward Nguyen</b> Software Engineer
          </span>
        </div>
        <p>
          Một chú IT biết code, biết viết, biết sửa tủ lạnh, điều hòa, máy giặt, khoan tường đẽo gỗ và vô số trò nghịch phá linh tinh để thỏa mãn trí tò mò. Ngoài
          việc thích trời Hà Nội đầu đông thì cũng rất thích mèo ta và chó cỏ. Có thể dành cả buổi chiều nằm dài ra ngoài đồng giữa mùa gió tháng mười và ngồi thừ
          cả đêm ngoài Circle K những ngày đầu hè tẻ nhạt.
        </p>
        <div class="flex mt-20">
          <a href="https://www.facebook.com/monokaijssss" target="_blank">
            <FacebookIcon width=30/>
          </a>
          <a href="https://www.linkedin.com/in/monokaijs/" target="_blank">
            <LinkedInIcon width=30/>
          </a>
        </div>
      </div>
    </div>
  </div>
</main>
