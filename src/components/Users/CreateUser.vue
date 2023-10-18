<template>
  <div>
    <h1>Create Users</h1>
    <form v-on:submit.prevent="createUser">
      <p>namebook: <input type="text" v-model="user.name" /></p>
      <p>type: <input type="text" v-model="user.lastname" /></p>
      <p>price: <input type="text" v-model="user.price" /></p>
      <p><button type="submit">create user</button></p>
    </form>
    <hr />
    <div>
      <p>name: {{ user.name }}</p>
      <p>lastname: {{ user.lastname }}</p> 
      <p>price: {{ user.price }}</p>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UserService";

export default {
  data() {
    return {
      user: {
        name: "",
        lastname: "",
        email: "",
        password: "",
        status: "active"
      }
    };
  },
  methods: {
    async createUser() {
      try {
        await UsersService.post(this.user);
        this.$router.push({
          name: "users"
        });
      } catch (err) {
        console.log(err);
      }
    }
  }
};
</script>
<style scoped></style>
