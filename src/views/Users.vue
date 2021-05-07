<template>
  <h2>Users</h2>

  <ul class="list-group col-4">
    <li
      v-for="user in users"
      @click.prevent="userData(user)"
      :key="user.id"
      class="list-group-item d-flex justify-content-between"
    >
      <router-link
        :to="'/users/' + user.first_name.toLowerCase()"
        class="list-group-item list-group-item-action"
      >
        {{ user.first_name }}
      </router-link>
      <button
        @click="removeLink(user)"
        type="button"
        class="btn btn-danger mx-3"
      >
        Delete
      </button>
    </li>
    <button
      v-if="clickDel"
      @click="getUsers"
      type="button"
      class="btn btn-primary my-3"
    >
      Update
    </button>
  </ul>
</template>

<script>
export default {
  name: "Users",
  data() {
    return {
      users: [],
      clickDel: false,
    };
  },
  methods: {
    userData(user) {
      localStorage.clear();
      localStorage.setItem("user", JSON.stringify(user));
      this.$store.state.user = user;
    },
    removeLink(user) {
      this.users = this.users.filter((el) => el !== user);
      this.clickDel = true;
    },

    async getUsers() {
      try {
        const response = await fetch("https://reqres.in/api/users?page=1");
        const json = await response.json();
        this.users = json.data;
      } catch (error) {
        console.log(error);
      }
      this.clickDel = false;
    },
  },
  created() {
    this.getUsers();
  },
};
</script>

<style>
</style>