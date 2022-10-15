<template>
  <div class="page">
    <h1>Welcome</h1>
    <router-link to="/login"><button class="ctn">Go Back</button></router-link>
  </div>
  <!-- <table>
    <tr>
      <td>Id</td>
      <td>avatar</td>
      <td>email</td>
      <td>first_name</td>
      <td>last_name</td>
    </tr>
    <tr v-for="item in pic" :key="item.id">
    <td>{{item.id}}</td>
    <td>{{item.avatar}}</td>
    <td>{{item.email}}</td>
    <td>{{item.first_name}}</td>
    <td>{{item.last_name}}</td>
  </tr>
  </table> -->
</template>

<script>
import axios from "axios";
export default {
  name: "Page",
  components: {},
  data() {
    return {
      name: "",
    };
  },
  mounted(){
      let user = localStorage.getItem('user-info');
      if(!user){
          this.$router.push({name:'signup'})
      }
  }

  
  // async mounted() {
  //   let user = localStorage.getItem("user-info");
  //   this.name = JSON.parse(user).name;
  //   if (!user) {
  //     this.$route.push({ name: "login" });
  //   }
  // },
};
</script>

<style lang="scss">
@import "@/assets/scss/main.scss";
.page {
  text-align: center;
  border: 5px solid $black;
  padding: 3rem;

  font-size: 4.5rem;

  & button {
    margin-top: 2rem;
    font-size: 3rem;
    cursor: pointer;
    transition: background 0.3s ease-in-out;
    animation-fill-mode: both;
  animation-duration: 1s;

    &:hover {
      animation-name: shake;
    }
  }

  @keyframes shake {
  0%, 100% {
    transform: translateX(0); }
  10%, 30%, 50%, 70%, 90% {
    transform: translateX(-10px); }
  20%, 40%, 60%, 80% {
    transform: translateX(10px); }
}
}
</style>
