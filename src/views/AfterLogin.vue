<template>
  <div class="after-login">
    <a href="">home</a>
    <a href="">add</a>
    <a href="">update</a>
    <!-- <a href="#login">Logout</a> -->
    <router-link to="/login">Logout</router-link>
    <div class="add-data">
      <input v-model="id" type="text" placeholder="Enter Id" name="id" />
      <input v-model="email" type="text" placeholder="Enter Email" name="email" />
      <input v-model="firstName" type="text" placeholder="Enter First Name" name="First Name" />
      <input v-model="lastName" type="text" placeholder="Enter Last Name" name="Last Name" />
      <input  type="file" accept="image/png, image/jpeg" />
      <button @click="addData">Add</button>
    </div>
    <table>
      <tr>
        <th>id</th>
        <th>avatars</th>
        <th>email</th>
        <th>first name</th>
        <th>last name</th>
        <th>Edit</th>
      </tr>
      <tr v-for="item in list" :key="item.id">
        <td>{{ item.id }}</td>
        <td><img :src="item.avatar" /></td>
        <td>{{ item.email }}</td>
        <td>{{ item.first_name }}</td>
        <td>{{ item.last_name }}</td>
        <td></td>
      </tr>
    </table>
  </div>
  <Footer></Footer>
</template>

<script>


import axios from "axios";

export default {
  name: "Home",
  components: {
  },
  data() {
    return {
      list: [],
      add: {
        id: "",
    avatar: "",
    email: "",
    firstName: "",
    lastName: "",
        
      }
    };
  },

  methods: {
    // logout() {
    //   localStorage.clear();
    //   this.$router.push({ name: "login" });
    // },
    addData(data) {
        axios.post('https://reqres.in/api/users', {
name: this.name,
email:this.email,
firstName: this.firstName,
lastName: this.lastName,

        })
        console.log(data);
    }
  },

  async mounted() {
    let results = await axios.get("https://reqres.in/api/users");
    console.log("results", results);
    this.list = results.data.data;
    let user = localStorage.getItem("user-info");
    this.name = JSON.parse(user).name;
    if (!user) {
      this.$route.push({ name: "login" });
    }
  },
};
</script>

<style lang="scss">
@import "@/assets/scss/main.scss";

.after-login {
  table {
    border-collapse: collapse;
    text-align: center;
    margin-top: 15px;
  }

  td {
    width: 150px;
    height: 40px;
    font-size: 1rem;
    border: 2px solid $gray;
  }

  th {
    font-size: 1.5rem;
    border: 2px solid $gray;
  }

  img {
    width: 70px;
    height: 70px;
    border-radius: 50%;
  }
}

.add-data {
  & input {
    @include input;
    margin-bottom: 20px;
    padding-left: 20px;
    display: block;
    margin-left: auto;
    margin-right: auto;
    height: 40px;
    width: 300px;

    &:nth-last-child(2) {
      border: none;
    }
  }

  & button {
    @include button-ctn;
    width: 320px;
    height: 40px;
    margin-bottom: 20px;
    padding-left: 20px;
    display: block;
    margin-left: auto;
    margin-right: auto;
  }
}
</style>
