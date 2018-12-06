<template>
    <div id="single-blog">
        <h1>{{ blog.title}}</h1>
        <article> {{ blog.content }}</article>
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
</style>
