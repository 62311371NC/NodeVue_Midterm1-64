<template>
  <div>
    <h1>Show Projector</h1>
    <p>id: {{ userId }}</p>
    <p>ชื่อรุ่น  {{ user.name }} - {{ user.lastname }}</p>
    <p>สเปค Projector: {{ user.email }}</p>
    <p>ราคา: {{ user.password }}</p>
  </div>
</template>
<script>
import UserService from "@/services/UsersService";
export default {
  data() {
    return {
      user: null,
    };
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UserService.show(userId)).data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
<style scoped>
</style>