<template>
  <div class="container">
    <div class="post">
      <h2>{{ post.title.rendered }}</h2>
      <div v-html="post.content.rendered"></div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      post: {}
    }
  },
  asyncData({ params, payload }) {
    if (payload) {
      return {
        post: payload
      }
    } else {
      return axios
        .get('http://vuejs-wordpress:8888/wp-json/wp/v2/posts/' + params.id)
        .then((res) => {
          return {
            post: res.data
          }
        })
    }
  }
}
</script>

<style scoped></style>
