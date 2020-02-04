<template>
  <div class="container">
    <article>
      <h1 class="title">What is Balut?</h1>
      <p>
        If someone placed balut on your plate, you might think they were serving
        you a hardboiled egg. That is, until you cracked it open and a fully
        intact duck embryo spilled out. Balut, considered a delicacy in many
        Asian countries, is produced when fertilized duck eggs are placed in
        warm sunlight. After about eight days, the eggs are held up to the light
        and checked to ensure that the budding embryo is ready. Then, the eggs
        are cooked and served with a dash of salt and a few squirts of lemon
        juice.
      </p>
    </article>
  </div>
</template>

<script>
export default {
  asyncData(context) {
    // called every time before loading the component
    // as the name said, it can be async
    // Also, the returned object will be merged with your data object
    return { name: 'World' }
  },
  fetch() {
    // The `fetch` method is used to fill the store before rendering the page
  },
  head() {
    // Set Meta Tags for this Page
  }
  // and more functionality to discover
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
