<template>
  <div class="after-login">
    <!-- <a href="#login">Logout</a> -->
    <router-link to="/login" class="ctn btn-logout">Logout</router-link>
    
    <table>
      <tr>
        <th>id</th>
        <th>avatars</th>
        <th>email</th>
        <th>first name</th>
        <th>last name</th>
      </tr>
      <tr v-for="item in list" :key="item.id">
        <td>{{ item.id }}</td>
        <td><img :src="item.avatar" /></td>
        <td>{{ item.email }}</td>
        <td>{{ item.first_name }}</td>
        <td>{{ item.last_name }}</td>
      </tr>
    </table>

  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Home",
  components: {},
  data() {
    return {
      list: [],
     
    };
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
    width: 40rem;
    height: 40px;
    font-size: 1rem;
    border: 2px solid $gray;
    text-align: center;


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


.btn-logout {
 display: block;;
  margin: 30px;
  text-align: center;
  justify-items: center;
  align-items: center;
}

</style>
