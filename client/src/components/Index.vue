<template>
  <div>
    <h1>Projector</h1>
    <div v-if="users.length">
      <h4>จำนวนผู้ใช้งาน {{ users.length }}</h4>
      <p>
        <button v-on:click="navigateTo('/user/create')">
            สร้างเครื่องฉายภาพ
          </button>
      </p>
      <div v-for="user in users" v-bind:key="user.id">
        <p>IDProjector: {{ user.id }}</p>
        <p>ชื่อรุ่น: {{ user.name }} - {{ user.lastname }}</p>
        <p>สเปค Projector: {{ user.email }}</p>
        <p>ราคา: {{ user.password }}</p>
        <p>
          <button v-on:click="navigateTo('/user/' + user.id)">
            ดูข้อมูล Projector
          </button>
          <button v-on:click="navigateTo('/user/edit/' + user.id)">
            แก้ไขข้อมูล
          </button>
          <button v-on:click="deleteUser(user)">
            ลบข้อมูล
          </button>
        </p>
        <hr />
      </div>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      users: [],
    };
  },
  async created() {
    try {
      this.users = (await UsersService.index()).data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteUser(user){
      let result = confirm("Want to delete")
      if(result){
        try{
          await UsersService.delete(user)
          this.refreshData()
        }catch(error){
          console.log(error)
        }
      }
    },
    async refreshData(){
      this.users = (await UsersService.index()).data
    }
  },
};
</script>
<style scoped>
</style>