<template>
  <div class="product-display">
    <div class="Product">
      <h1 @click="toggleVisiblity">{{ Project.title }}</h1>
      <div class="icons">
        <span class="material-icons" @click="deletee"> delete </span>
        <span class="material-icons" @click="toggleComplete"> done </span>
        <router-link :to="{ name: 'EditProject', params: { id: Project.id } }">
          <span class="material-icons"> edit</span>
        </router-link>
      </div>
    </div>
    <h3 class="details" v-if="visibility">{{ Project.details }}</h3>
  </div>
</template>

<script>
export default {
  props: ["Project"],
  data() {
    return {
      visibility: false,
      uri: "http://localhost:3000/projects/" + this.Project.id,
    };
  },
  methods: {
    toggleVisiblity() {
      this.visibility = !this.visibility;
    },
    deletee() {
      fetch(this.uri, {
        method: "DELETE",
      })
        .then(() => this.$emit("deleted", this.Project.id))
        .catch((err) => console.log(err));
    },
    toggleComplete() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ complete: !this.Project.complete }),
      }).then(() => {
        this.$emit("completed", this.Project.id);
      });
    },
  },
};
</script>

<style>
.product-display {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.Product {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 120px;
  border-radius: 20px;
  width: 70vw;
  margin: 20px;

  border: 2px solid rgb(255, 255, 255);
}
.Product h1 {
  font-weight: 300;
}
.icons {
  margin: 0px 20px;
}
.Product h1 {
  margin: 0px 20px;
}
h3 {
  font-weight: 100;
  font-size: 2rem;
}
span {
  transform: scale(1.4);
  margin: 0px 10px;
}
</style>
