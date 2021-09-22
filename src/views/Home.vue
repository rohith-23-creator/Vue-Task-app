<template>
  <div class="home">
    <FilterProject @FilterChange="current = $event" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @deleteEvent="delete"
          @complete="completeEvent"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject.vue";
import FilterProject from "../components/FilterProject.vue";
export default {
  name: "Home",
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  components: {
    SingleProject,
    FilterProject,
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    delete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      });
    },
    completeEvent(id) {
      let p = this.projects.find((project) => {
        return project.id === id;
      });
      p.completed = !p.completed;
    },
  },
  computed: {
    filteredProjects() {
      if (this.current === "completed") {
        return this.projects.filter((project) => project.completed);
      }
      if (this.current === "ongoing") {
        return this.projects.filter((project) => !project.completed);
      }
      return this.projects;
    },
  },
};
</script>
