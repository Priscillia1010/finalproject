<template>
  <div class="container">
    <form @submit.prevent="addItem">
      <h2>Add New Item</h2>
      <p>New Shoes Take You Good Place!</p>
      <div class="inputContaner">
        <label for="title">Title</label>
        <input type="text" placeholder="Title" id="title" v-model="title" />
      </div>
      <div class="inputContaner">
        <label for="price">Price</label>
        <input type="text" placeholder="Price" id="price" v-model="price" />
      </div>
      <div class="inputContaner">
        <label for="file">Image Link</label>
        <input type="text" id="file" placeholder="Image Link" v-model="iamge" />
      </div>
      <button>Submit</button>
    </form>
    <nuxtLink class="back" to="/">Back</nuxtLink>
  </div>
</template>
<script>
export default {
  data() {
    return {
      title: "",
      price: "",
      image: "",
    };
  },
  middleware: ["check-auth", "auth"],
  method: {
    addItem() {
      if (
        this.title.length > 0 &&
        this.price.length > 0 &&
        this.image.length > 0
      ) {
        this.$store
          .dispatch("addShoes", {
            title: this.title,
            price: this.price,
            image: this.image,
          })
          .then(() => this.$router.push("/"));
      } else {
        alert("Please fill the form");
      }
    },
  },
};
</script>
<style scoped>
.container {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: "Lexend Deca", sans-serif;
  background: url("../../static/assets/star.png"), #e6e6e6;
  text-align: center;
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  padding: 1rem;
}

form > * {
  padding: 0;
  margin: 0;
}

form h2 {
  font-size: 64px;
}

form input,
form button {
  padding: 12px 21px;
  color: white;
  border: none;
  outline: none;
  border-radius: 10px;
  width: 500px;
  background-color: #224957;
  box-sizing: border-box;
}

button {
  background-color: #20df7f !important;
  color: black !important;
}

form input::placeholder {
  color: white;
}

a {
  color: black;
  text-decoration: none;
}

.back {
  position: absolute;
  top: 5%;
  left: 5%;
  padding: 0.5rem 1rem;
  border: none;
  outline: none;
  background-color: #224957 !important;
  color: white !important;
  border-radius: 100px;
  cursor: pointer;
}

.inputContainer {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  gap: 0.5rem;
}

@media only screen and (max-width: 600px) {
  form h2 {
    font-size: 40px;
  }
}

@media only screen and (max-width: 500px) {
  form button {
    width: 100%;
  }
  form input {
    width: calc(100vw - 2rem);
  }
}

@media only screen and (max-width: 350px) {
  form h2 {
    font-size: 30px;
  }
}
</style>
