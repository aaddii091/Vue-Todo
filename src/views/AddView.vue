<template>
  <div>
    <h1>ADD PROJECT</h1>
    <form @submit.prevent="formSubmit">
      <label>Title</label>
      <input
        type="text"
        required
        placeholder="Enter Your Title"
        v-model="title"
      />
      <label>Description</label>
      <input
        type="text"
        required
        placeholder="Enter Description"
        v-model="details"
      />
      <button>Add Project</button>
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
    formSubmit() {
      let project = {
        title: this.title,
        details: this.details,
        complete: false,
      };
      fetch("http://localhost:3000/projects", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(project),
      }).then(() => {
        this.$router.push("/");
      });
    },
  },
};
</script>

<style>
h1 {
  text-align: center;
  margin: 50px 0px;
  font-size: 3rem;
  font-weight: 100;
}
form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
input {
  min-width: 40vw;
  height: 50px;
  margin: 20px 0px;
}
input::placeholder {
  font-size: 1.5rem;
}
input[type="text"] {
  color: black;
  font-size: 1.5rem;
  font-family: "Roboto", sans-serif;
}
label {
  font-size: 2rem;
  font-weight: 100;
}
button {
  padding: 15px 35px;
  border-radius: 25px;
  color: black;
  font-size: 1.1rem;
  margin-top: 15px;
}
</style>
