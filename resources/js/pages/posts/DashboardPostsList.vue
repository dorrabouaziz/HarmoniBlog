<template class="categories-list">
  <div>
    <h1>Posts List</h1>
    <!-- success message -->
    <div class="success-msg" v-if="success">
      <i class="fa fa-check"></i>
      Post deleted successfully
    </div>
    <div class="success-msg" v-if="editSuccess">
      <i class="fa fa-check"></i>
      Post edited successfully
    </div>

    <!-- Display posts as cards in rows -->
<div class="grid-container">
  
  <div class="col-md-4" v-for="(post, index) in posts" :key="post.id">
    <div class="card " style="width: 18rem; margin: 15px;">
      <img :src="post.imagePath" >
      <div class="card-body">
        <h5 class="card-title">{{ post.title }}</h5>
        <p class="card-text">{{ post.body }}</p>
        <div class="button-container">
          <router-link class="edit-link" :to="{ name: 'EditPosts', params: { slug: post.slug } }">
            Edit
          </router-link>
          <button @click="destroy(post.slug)" class="delete-btn">
            Delete
          </button>
        </div>
      </div>
    </div>
    
    <!-- Add a new row after every third card -->
    <div v-if="index % 3 === 2" class="w-100"></div>
  </div>
</div>


    <!-- Create Post link -->
    <div class="index-categories">
      <router-link :to="{ name: 'CreatePosts' }" class="btn btn-create-posts">
        Create Post<span>&#8594;</span>
      </router-link>
    </div>
  </div>
</template>


<script>
export default {
  props: ["editSuccess"],
  emits: ["updateSidebar"],
  data() {
    return {
      posts: [],
      success: false,
    };
  },
  methods: {
    destroy(slug) {
      axios
        .delete(`/api/posts/${slug}`)
        .then(() => {
          this.fetchPosts();
          this.success = true;
          setTimeout(() => {
            this.success = false;
          }, 2500);
        })
        .catch((error) => {
          console.log(error.response.data);
        });
    },

    fetchPosts() {
      axios
        .get("/api/dashboard-posts")
        .then((response) => (this.posts = response.data.data))
        .catch((error) => {
          console.log(error);
        });
    },
  },

  mounted() {
    this.fetchPosts();
  },
};
</script>

<style scoped>
.categories-list {
  min-height: 100vh;
  background: #fff;
}

.categories-list h1 {
  font-weight: 300;
  padding: 50px 0 30px 0;
  text-align: center;
}

.categories-list .card {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.categories-list .card-body {
  padding: 15px;
}

.button-container {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}

.index-categories {
  text-align: center;
}
.grid-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
}

</style>