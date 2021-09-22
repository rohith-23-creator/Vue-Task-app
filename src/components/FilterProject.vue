<template>
  <div class="filter-nav">
    <button :class="{ active: current === 'all' }" @click="updateFilter('all')">
      All
    </button>
    <button
      :class="{ active: current === 'completed' }"
      @click="updateFilter('completed')"
    >
      Completed
    </button>
    <button
      :class="{ active: current === 'ongoing' }"
      @click="updateFilter('ongoing')"
    >
      Ongoing
    </button>
  </div>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    updateFilter(param) {
      this.$emit("filterChange", param);
    },
  },
};
</script>

<style scoped>
.filter-nav button {
  border: none;
  font-size: 12px;
  font-weight: bold;
  margin-right: 10px;
  background: none;
  /* border-bottom: 2px solid #fff; */
  outline: none;
  border-radius: 0;
  opacity: 0.8;
}

.filter-nav button.active {
  color: #9277ff;
  opacity: 1;
  border-bottom: 2px solid #9277ff;
}

@media (max-width: 300px) {
  .filter-nav {
    margin: 2rem 0;
    align-items: center;
    justify-content: center;
    text-align: center;
    display: flex;
  }
  .filter-nav button {
    margin-right: 5px;
    font-size: 10px;
  }
}
</style>
