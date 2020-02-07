<template>
  <div class="container">
    <article>
      <h1 class="title">{{ post.title }}</h1>
      <p>{{ post.content }}</p>
    </article>
    <aside>
      <h3>Posts you might enjoy</h3>
      <ul>
        <li v-for="related in relatedPosts" :key="related.title">
          <nuxt-link :to="{ name: 'posts-id', params: { id: related.id } }">
            {{ related.title }}
          </nuxt-link>
        </li>
      </ul>
    </aside>
  </div>
</template>

<script>
export default {
  data() {
    return {
      id: this.$route.params.id
    }
  },
  computed: {
    post() {
      // return this.posts.find((post) => post.id === this.id)
      // Let's use the posts coming from the store in our component.
      // Here, we used to access the posts under this.posts.
      // Now, we have to access the store.
      // Nuxt has automatically injected the store into all components.
      // So, we can use this.$store, then navigate to the state, then the posts module, and grab all the posts that live in the all property.
      return this.$store.state.posts.all.find((post) => post.id === this.id)
    },
    relatedPosts() {
      // return this.posts.filter((post) => post.id !== this.id)
      // Let's do the same for the recommended posts.
      // Notice here that there is no difference, on how you use Vuex in your application.
      return this.$store.state.posts.all.filter((post) => post.id !== this.id)
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
