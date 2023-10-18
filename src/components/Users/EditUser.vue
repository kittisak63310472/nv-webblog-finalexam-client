<template>
  <div>
    <h1>Edit Users</h1>
    <h1>Edit User</h1>
    <form v-on:submit.prevent="editUser">
      <p>namebook: <input type="text" v-model="user.name" /></p>
      <p>type: <input type="text" v-model="user.lastname" /></p>
      <p>price: <input type="text" v-model="user.price" /></p>
      <p><button type="submit">edit user</button></p>
    </form>
    <hr />
    <div>
      <p>name: {{ user.name }}</p>
      <p>lastname: {{ user.lastname }}</p> 
      <p>price: {{ user.price }}</p>
      <p></p>
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
    async editUser() {
      try {
        await UsersService.put(this.user);
        this.$router.push({
          name: "users"
        });
      } catch (err) {
        console.log(err);
      }
    }
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UsersService.show(userId)).data;
    } catch (error) {
      console.log(error);
    }
  }
};
</script>
<style scoped></style>
