<template>
  <div class="container">
    <form @submit.prevent="submitForm">
      <div class="input-title">
        <label for="title">Title</label>
        <input v-model="title" type="text" required />
      </div>
      <div class="input-details">
        <label for="title">Details</label>
        <textarea v-model="details" cols="15" rows="5" required></textarea>
      </div>
      <div class="submit-btn">
        <button type="submit">
          Add Task
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      details: "",
    };
  },
  methods: {
    submitForm() {
      let project = {
        title: this.title,
        details: this.details,
        completed: false,
      };
      fetch("http://localhost:3000/projects", {
        method: "POST",
        headers: { "Content-type": "application/json" },
        body: JSON.stringify(project),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => console.log(err.message));
      console.log(project);
      // this.details = " ";
      // this.title = " ";
    },
  },
};
</script>

<style>
.container {
  width: 100%;
  height: 70vh;
  margin: auto;
  display: flex;
  flex-direction: column;
  color: #fff;
}

form {
  background-color: #1e2139;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  text-align: left;
  padding: 2rem;
  color: #ffff;
  width: 30rem;
  margin: auto;
}

.input-title,
.input-detail {
  margin-bottom: 2rem;
}

input,
textarea {
  font-size: 16px;
  background-color: #141625;
  color: #ffff;
  border-radius: 3px;
  border: 1px solid #141625;
  outline: 1px solid #141625;
  width: 100%;
  font: inherit;
  padding: 5px;
  font-size: 15px;
}
input:focus,
textarea:focus {
  border: 1px solid #5d3af8;
  outline: 1px solid #5d3af8;
}

input {
  padding: 10px 05px;
}

label {
  display: block;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

textarea {
  resize: none;
  margin-bottom: 2rem;
}

button {
  position: relative;
  background-color: #5d3af8;
  color: #fff;
  padding: 10px 20px;
  border-radius: 30px;
  border: none;
  font: inherit;
  outline: none;
  font-size: 14px;
  font-weight: bold;
  cursor: pointer;
}

button:hover {
  opacity: 0.8;
}

@media (max-width: 700px) {
  form {
    width: 25rem;
  }
}

@media (max-width: 500px) {
  form {
    width: 20rem;
  }
}

@media (max-width: 400px) {
  form {
    width: 17rem;
  }
}
</style>
