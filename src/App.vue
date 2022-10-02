<template>
  <div>
    <ul v-for="post in posts" v-bind:key="post.id">
      <li>
        <h2>{{ post.title.rendered }}</h2>
      </li>
      <p>{{ post.content.rendered }}</p>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [],
    };
  },
  methods: {
    async getData() {
      try {
        let response = await fetch(
          "http://localhost/wordpress/wp-json/wp/v2/posts"
        );
        this.posts = await response.json();
      } catch (error) {
        console.log(error);
      }
    },
  },
  created() {
    this.getData();
  },
};
</script>
