<template>
  <div class="home" v-if="projects.length">
    <div v-for="project in projects" :key="project.id">
      <SingleProduct
        :Project="project"
        @deleted="handleDelete"
        @completed="complete"
      />
    </div>
  </div>
</template>

<script>
import SingleProduct from "../components/SingleProject.vue";
export default {
  name: "HomeView",
  components: { SingleProduct },
  data() {
    return {
      projects: [],
    };
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((p) => {
        return p.id !== id;
      });
    },
    complete(id) {
      let p = this.projects.find((pro) => {
        return pro.id === id;
      });
      p.complete = !p.complete;
    },
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err));
  },
};
</script>
<style>
/* .home {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  margin: 0px auto;
} */
</style>
