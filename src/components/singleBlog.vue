<template>
    <div id="single-blog">
        <h1>{{ blog.title}}</h1>
        <p><strong>{{ blog.author }}</strong></p>
        <article> {{ blog.content }}</article>
        <ul>
            <li><strong>Categories:</strong></li>
            <li v-for="category in blog.categories" :key=category>{{ category }}</li>
        </ul>
    </div>
</template>

<script>

export default {
    data() {
        return {
            id: this.$route.params.id,
            blog: {
            }
        }
    },
    async created() {
        try {
            let res = await this.axios.get(`https://nn-vue-playlist-374cd.firebaseio.com/posts/${this.id}.json`)
            this.blog = res.data
        } catch (err) {
            console.log(err)
        }
    }
}
</script>

<style scoped>
#single-blog {
    max-width: 960px;
    margin: 0 auto;
}
ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
}
</style>
