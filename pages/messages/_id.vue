<template>
  <div class="container">
    <article>
      <h1 class="title">{{ message.title }}</h1>
      <p>{{ message.content }}</p>
    </article>
    <aside>
      <h3>Posts you might enjoy</h3>
      <ul>
        <li v-for="related in relatedMessages" :key="related.title">
          <nuxt-link :to="{ name: 'messages-id', params: { id: related.id } }">
            {{ related.title }}
          </nuxt-link>
        </li>
      </ul>
    </aside>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: this.message.title,
      meta: [
        { name: 'twitter:title', content: this.message.title },
        { name: 'twitter:description', content: this.message.content },
        { name: 'twitter:image', content: 'https://i.imgur.com/UYP2umJ.png' },
        { name: 'twitter:card', content: 'summary_large_image' }
      ]
    }
  },
  data() {
    return {
      id: this.$route.params.id
    }
  },
  computed: {
    message() {
      // return this.posts.find((post) => post.id === this.id)
      // Let's use the posts coming from the store in our component.
      // Here, we used to access the posts under this.posts.
      // Now, we have to access the store.
      // Nuxt has automatically injected the store into all components.
      // So, we can use this.$store, then navigate to the state, then the posts module, and grab all the posts that live in the all property.
      return this.$store.state.messages.all.find(
        (message) => message.id === this.id
      )
    },
    relatedMessages() {
      // return this.posts.filter((post) => post.id !== this.id)
      // Let's do the same for the recommended posts.
      // Notice here that there is no difference, on how you use Vuex in your application.
      return this.$store.state.messages.all.filter(
        (message) => message.id !== this.id
      )
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  line-height: 1.5;
}
article * {
  margin-bottom: 1rem;
}
aside {
  min-width: 280px;
  max-width: 280px;
  padding-left: 2rem;
}
.title {
  font-size: 2rem;
}
</style>
