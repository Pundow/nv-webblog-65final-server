<template>
	<div>
		<div class="container">
		<h1>Show Blog</h1>
		<p>id: {{ blog.id }}</p>
		<p>title: {{ blog.title }}</p>
		<p>content: {{ blog.content }}<div class="content" v-html="blog.content"></div></p>
		<p>category: {{ blog.category }}</p>
		<p>status: {{ blog.status }}</p>
		<p>
			<button v-on:click="navigateTo('/blog/edit/' + blog.id)">
				แก้ไข blog
			</button>
			<button v-on:click="navigateTo('/blogs')">กลับ</button>
		</p>
	</div>
</div>
</template>
<script>
   import BlogsService from '@/services/BlogsService'
   import UsersService from '@/services/UsersService'
   export default {

    data () {
    return {
    blog: null,
    resultUpdated: '',
    users:null
    }
    },
    delete () {
    console.log('delete blog')
    },
    async created () {
    // get blog
    // check permission first
    try {
    let blogId = this.$route.params.blogId
    this.blog = (await BlogsService.show(blogId)).data
    } catch (error) {
    console.log (error)
    }
    },
    methods: {
    navigateTo (route) {this.$router.push(route)
    },
    }
   }
   </script>
<style scoped>


</style>
