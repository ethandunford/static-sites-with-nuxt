<template>
    <section class="container">
        <h2>This is a Homepage</h2>

        <div class="posts">
            <h3>Latest from our Blog</h3>

            <div class="post" v-for="post in posts" :key="post.id">
                <h4>{{ post.title.rendered }}</h4>

                <div class="post-content" v-html="post.excerpt.rendered" />
                <nuxt-link :to="{ name: 'blog-slug', params: { slug: post.slug, id: post.id } }">
                    Read More
                </nuxt-link>
            </div>
        </div>
    </section>
</template>

<script>
    import axios from 'axios'

    export default {
        fetch({ store }) {
            return axios.get('http://nuxt-wp.localhost/wp-json/wp/v2/posts').then((res) => {
                store.commit('frontPagePosts', res.data)
            }).catch((error) => {
                console.log(error)
            })
        },
        computed: {
            posts() {
                return this.$store.state.posts
            }
        }
    }
</script>

<style lang="scss">
    .container {
        margin: 0 auto;
        width: 960px;
        border-bottom: 1px solid red;
    }
</style>
