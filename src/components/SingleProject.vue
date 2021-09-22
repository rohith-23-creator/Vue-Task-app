<template>
  <NavBar />
  <div class="project" :class="{ complete: project.completed }">
    <div class="actions">
      <div class="header" @click="showDetails()">
        <h3>{{ project.title }}</h3>
      </div>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }">
          <span class="material-icons" style="color:#9277ff"> edit</span>
        </router-link>

        <span class="material-icons" style="color: red;" @click="deleteProject">
          delete</span
        >
        <span class="material-icons tick" @click="toggleComplete"> done</span>
      </div>
    </div>
    <div class="details" v-if="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],

  data() {
    return {
      details: false,
      url: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    showDetails() {
      return (this.details = !this.details);
    },

    deleteProject() {
      fetch(this.url, { method: "DELETE" })
        .then(() => this.$emit("deleteEvent", this.project.id))
        .catch((err) => console.log(err.message));
    },
    toggleComplete() {
      fetch(this.url, {
        method: "PATCH",
        headers: { "Content-type": "application/json" },
        body: JSON.stringify({ completed: !this.project.completed }),
      })
        .then(() => {
          this.$emit("complete", this.project.id);
        })
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style scoped>
.project {
  margin: 20px auto;
  background-color: #1e2139;
  padding: 10px 20px;
  border-radius: 4px;
  border-left: 3px solid #e90074;
  position: relative;
}

.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.header {
  flex: 60%;
}

.material-icons {
  margin-left: 10px;
  cursor: pointer;
  color: #ffff;
  opacity: 0.8;
}

.material-icons:hover {
  color: green;
}

h3 {
  font-size: 16px;
  cursor: pointer;
  color: #ffff;
  opacity: 0.8;
}

p {
  font-size: 14px;
  line-height: 1.8;
  color: #9277ff;
}

.project.complete {
  border-left: 3px solid green;
}

.project.complete .tick {
  color: green;
}

@media (max-width: 450px) {
  h3 {
    font-size: 15px;
  }

  p {
    font-size: 13px;
  }

  .material-icons {
    font-size: 20px;
  }
}

@media (max-width: 350px) {
  .header {
    flex: 80%;
  }
  .material-icons {
    font-size: 16px;
  }

  h3 {
    font-size: 14px;
  }
}
</style>
