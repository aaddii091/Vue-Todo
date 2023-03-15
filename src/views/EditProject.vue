<template>
  <div>
    <h1>EDIT PROJECT</h1>
    <h2>{{ $route.params.id }}</h2>
    <form @submit.prevent="formSubmit">
      <label>Title</label>
      <input type="text" required v-model="title" />
      <label>Description</label>
      <input type="text" required v-model="details" />
      <button>save</button>
    </form>
  </div>
</template>

<script>
export default {
  //   props: [id],
  data() {
    return {
      title: "",
      details: "",
      uri: "http://localhost:3000/projects/" + this.$route.params.id,
    };
  },
  mounted() {
    fetch(this.uri, {}).then((res) => {
      res.json().then((data) => {
        (this.title = data.title), (this.details = data.details);
      });
    });
  },
  methods: {
    formSubmit() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ title: this.title, details: this.details }),
      })
        .then(() => {
          this.$emit("completedEdit", this.$route.params.id);
        })
        .then(() => {
          this.$router.push("/");
        });
    },
  },
};
</script>

<style></style>
