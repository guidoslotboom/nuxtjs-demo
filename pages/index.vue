<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        nuxtjs-demo
      </h1>
      <h2 class="subtitle">
        My geometric Nuxt.js project
      </h2>
      <div class="links">
        <a href="https://nuxtjs.org/" target="_blank" class="button--green">
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
      <div class="links">
        <nuxt-link
          v-for="message in messages"
          :to="{ name: 'messages-id', params: { id: message.id } }"
          :key="message.id"
          class="button--grey"
        >
          {{ message.title }}
        </nuxt-link>
      </div>
      <div class="links">
        <h3>Latest posts from our Blog</h3>
        <ul>
          <li v-for="post in posts" :key="post.id">
            <h4>{{ post.title.rendered }}</h4>
            <div v-html="post.excerpt.rendered"></div>

            <nuxt-link
              :to="{
                name: 'blog-slug',
                params: { slug: post.slug, id: post.id }
              }"
            >
              Read more
            </nuxt-link>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  head() {
    return {
      title: 'Home Page 🍕',
      meta: [
        { name: 'twitter:title', content: 'Nuxt Fundamentals by Vue School' },
        { name: 'twitter:description', content: 'Nuxt + Vue School = 🍕' },
        { name: 'twitter:image', content: 'https://i.imgur.com/UYP2umJ.png' },
        { name: 'twitter:card', content: 'summary_large_image' }
      ]
    }
  },
  computed: {
    messages() {
      return this.$store.state.messages.all
    },
    posts() {
      return this.$store.state.posts
    }
  },
  fetch({ store }) {
    return axios
      .get('http://vuejs-wordpress:8888/wp-json/wp/v2/posts')
      .then((res) => {
        store.commit('frontPagePosts', res.data)
      })
      .catch((error) => {
        // eslint-disable-next-line
        console.log(error)
      })
  }
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  letter-spacing: 1px;
}
.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
}
.links {
  padding-top: 15px;
}
</style>
