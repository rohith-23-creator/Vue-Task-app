<template>
  <div class="nav">
    <div class="logo">
      <h1>Task App</h1>
    </div>
    <div class="btn-content">
      <router-link class="btn home-link" :to="{ name: 'Home' }"
        >Tasks</router-link
      >
      <router-link class="btn " :to="{ name: 'Form' }">Add New</router-link>
    </div>
  </div>
</template>

<style>
.nav {
  height: 20vh;
  width: 36rem;
  display: flex;
  justify-content: space-around;
  align-items: center;
  color: #fff;
}

.home-link {
  margin-right: 1rem;
}

h1 {
  font-size: 25px;
}

.btn {
  text-decoration: none;
  position: relative;
  background-color: #1e2139;
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

.btn:hover {
  opacity: 0.8;
}

.router-link-active {
  background-color: #7455fd;
}

@media (max-width: 700px) {
  .nav {
    align-items: center;
    text-align: center;
    justify-content: space-around;
    width: 90%;
    margin: auto;
  }

  h1 {
    font-size: 25px;
    margin-right: 1.5rem;
  }
}

@media (max-width: 500px) {
  .nav {
    width: 100%;
  }
  h1 {
    font-size: 20px;
    margin-right: 0.6rem;
  }

  .btn {
    font-size: 12px;
  }
  .home-link {
    margin-right: 0.6rem;
  }
}

@media (max-width: 300px) {
  .nav {
    flex-direction: column;
  }

  h1 {
    margin: 1rem 0;
  }

  .home-link {
    margin-left: 1rem;
    margin-right: 1rem;
  }
}
</style>
