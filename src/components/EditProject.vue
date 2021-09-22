<template>
  <div class="container">
    <form @submit.prevent="updateTask">
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
          Update
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: ["id"],

  data() {
    return {
      title: "",
      details: "",
      url: "http://localhost:3000/projects/" + this.id,
    };
  },
  mounted() {
    fetch(this.url)
      .then((res) => res.json())
      .then((data) => {
        (this.title = data.title), (this.details = data.details);
      });
  },
  methods: {
    updateTask() {
      fetch(this.url, {
        method: "PATCH",
        headers: { "Content-type": "application/json" },
        body: JSON.stringify({
          title: this.title,
          details: this.details,
        }),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => console.log(err.message));
    },
  },
};
</script>
