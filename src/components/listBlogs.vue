<template>
    <div v-theme:column="'wide'" id="show-blogs">
       <h1>List Blog Titles</h1>
       <input type="text" v-model="search" placeholder="Search blog posts"/>
       <div v-for="blog in filteredBlogs" class="single-blog" :key="blog.title">
           <h2 v-rainbow>{{ blog.title | toUpperCase}}</h2>
       </div>
    </div>
</template>

<script>
import searchMixin from '../mixins/searchMixin'
export default {

    data() {
        return {
            blogs: [],
            search: '',
        }
    },
    methods: {

    },
    mixins: [searchMixin],
    filters: {
        toUpperCase(value) {
            return value.toUpperCase()
        },
        snippet(value) {
            return value.slice(0, 100) + '...'
        }
    },
    directives: {
        'rainbow': {
            bind(el, binding, vnode) {
                el.style.color = `#${Math.random().toString().slice(2,8)}`
            }
        },
        'theme': {
            bind(el, binding, vnode) {
                if (binding.value === 'wide') {
                    el.style.maxWidth = '1200px'
                } else if (binding.value === 'narrow') {
                    el.style.maxWidth = '400px'
                }
                if (binding.arg === 'column') {
                    el.style.background = '#ddd'
                    el.style.padding = '20px'
                }
            }
        }
    },
    async created() {
        try {
            let res = await this.axios.get('https://jsonplaceholder.typicode.com/posts')
            this.blogs = res.data.slice(0, 10)
        } catch (err) {
            console.log(err)
        }
    }
}
</script>

<style>
#show-blogs {
    max-width: 800px;
    margin: 0 auto;
}

.single-blog {
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background-color: #eee;
}

</style>

