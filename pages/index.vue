<template>
  <div class="container mx-auto items-center flex">
    <div class="md:flex">
      <div class="flex flex-col justify-center md:w-3/4 text-center md:text-right">
        <!-- <h1 class="text-4xl">What's boo?</h1> -->
        <h2
          class="tracking-tight font-serif text-gray-700 text-3xl md:text-5xl"
        >A free and open source theme for headless Ghost CMS</h2>
        <p class="text-xl md:text-2xl text-gray-500 mt-5">Built with NuxtJS & TailwindCSS</p>
        <div class="mt-5">
          <nuxt-link :to="{path: '/blog'}" class="button">View posts</nuxt-link>
        </div>
      </div>
      <div class="md:w-1/2">
        <img class="w-48 md:w-64 mx-auto" src="~/assets/images/boo.svg" alt />
      </div>
    </div>
  </div>
</template>
<script>
import { ghost, postsPerPage, postIndexFields } from '../api/ghost'

import PostList from '../components/PostList'
export default {
	async asyncData({ params, store, error, payload }) {
		let pageginationPageNumber = 1
		if (params.pageNumber) {
			pageginationPageNumber = params.pageNumber
		}

		let paginationFilter = ''

		const posts = await ghost.posts.browse({
			limit: postsPerPage,
			page: pageginationPageNumber,
			include: 'tags,authors',
			fields: postIndexFields,
			filter: 'featured: true'
		})

		return {
			indexPosts: posts,
			indexPagination: posts.meta.pagination
		}
	},
	components: {
		PostList
	},
	methods: {}
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/

.title {
	display: block;
	font-weight: 300;
	font-size: 100px;
	color: #35495e;
	letter-spacing: 1px;
}
.links {
	padding-top: 15px;
}

.button {
	@apply shadow px-5 py-2 inline-block;
}
</style>
