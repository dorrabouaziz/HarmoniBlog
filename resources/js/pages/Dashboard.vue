<template>
<body>
 <div id="backend-view">
 <div class="logout">
    <a href="#" @click="logout">Log out</a>
 </div>
 <h1 class="heading">Dashboard</h1>
 <span>Hi {{ name }}!</span>


 <div class="links">
      <table class="table">
        <tr>
          <td>
            <button type="button" @click="navigateToCreatePosts" class="btn btn-primary">Create Posts</button>
          </td>
          <td>
            <button @click="navigateToDashboardPostsList" class="btn btn-custom-primary">Posts List</button>
          </td>
          <td>
            <button @click="navigateToCreateCategories" class="btn btn-custom-primary">Create Categories</button>
          </td>
          <td>
            <button @click="navigateToCategoriesList" class="btn btn-custom-primary">Categories List</button>
          </td>
        </tr>
      </table>
    </div>
  </div>

</body> 
</template>

<script>
export default {
  data() {
    return {
      name: "",
    };
  },
  mounted() {
    axios
      .get("/api/user")
      .then((response) => (this.name = response.data.name))
      .catch((error) => {
        if (error.response.status === 401) {
          this.$emit("updateSidebar");
          localStorage.removeItem("authenticated");
          this.$router.push({ name: "Login" });
        }
      });
  },

  methods: {
    logout() {
      axios
        .post("/api/logout")
        .then((response) => {
          this.$router.push({ name: "Home" });
          localStorage.removeItem("authenticated");
          this.$emit("updateSidebar");
        })
        .catch((error) => console.log(error));
    },

    navigateToCreatePosts() {
      this.$router.push({ name: 'CreatePosts' });
    },

    navigateToDashboardPostsList() {
      this.$router.push({ name: 'DashboardPostsList' });
    },

    navigateToCreateCategories() {
      this.$router.push({ name: 'CreateCategories' });
    },

    navigateToCategoriesList() {
      this.$router.push({ name: 'CategoriesList' });
    },
  },
};
</script>

<style scoped>
/* dashboard */
#backend-view {
  text-align: center;
  background-color: #f3f4f6;
  height: 100vh;
  padding-top: 15vh;
}

.logout {
  position: absolute;
  top: 30px;
  right: 40px;
}
.heading {
  margin-bottom: 5px;
}
.links {
  margin-top: 70px;
  margin-left: auto;
  margin-right: auto;
 
  max-width: 600px;
  padding: 15px;
  border-radius: 15px;
  height: 200px;

}
.links table {
  width: 100%;
}
.links td {
  padding: 10px;
}

/* Styles pour les boutons personnalisés */
button {
  margin-top: 40px;
  padding: 10px 20px; /* Ajustez la taille du bouton selon vos besoins */
  font-size: 16px;
  cursor: pointer;
  color: white;
  background-color: #007bff

}
#backend-view{
  background-size: cover;
  
  background: url('https://img.freepik.com/free-photo/shopping-center-out-focus_1194-1220.jpg?w=900&t=st=1705607401~exp=1705608001~hmac=f88cdc40416603750a8135f7424407382c4e56af9ba6ef9417437449319b1e5d') center no-repeat;
}

/* Ajoutez des styles supplémentaires selon vos préférences */
</style>