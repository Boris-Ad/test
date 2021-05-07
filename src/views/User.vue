<template>
<h3>User</h3>
  <div class="row">
    <div class="card col-4">
      <div class="card-body">
        <h5 class="card-title">Vuex</h5>
        <p
          class="card-text"
          v-for="(value, name, index) in $store.state.user"
          :key="index"
        >
          {{ name }} : {{ value }}
        </p>
      </div>
    </div>
    <div class="card col-4 mx-3">
      <div class="card-body">
        <h5 class="card-title">localStorage</h5>
        <p class="card-text" v-for="(value, name, index) in user" :key="index">
          {{ name }} : {{ value }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "User",
  data() {
    return {
      user: null,
    };
  },
  methods: {
    updateStorage() {
      let fer = localStorage.getItem("user");
      this.user = JSON.parse(fer);
    },
  },
  beforeUpdate() {
      this.updateStorage();
  },
  created() {
      this.updateStorage();
  },
};
</script>

<style>
</style>
 