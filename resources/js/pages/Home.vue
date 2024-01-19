<template>
  <!-- header -->
  <header class="header">
    <div class="header-text">
      <h1>HarmoniBlog</h1>
      <h4>Home of verified news...</h4>
    </div>
    <div class="overlay"></div>
  </header>
  
</template>
<script>
export default {
  emits: ["updateSidebar"],
  data() {
    return {
      posts: [],
    };
  },

  mounted() {
    axios
      .get("/api/home-posts")
      .then((response) => (this.posts = response.data.data))
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>