<template>
<div>
    <h1>Edit Projector</h1>
    <form v-on:submit.prevent = "editUser">
        <p>ชื่อรุ่น: <input type="text" v-model="user.name"></p>
        <p>เลขรุ่น: <input type="text" v-model="user.lastname"></p>
        <p>สเปค Projector: <input type="text" v-model="user.email"></p>
        <p>ราคา: <input type="text" v-model="user.password"></p>
        <p><button type="submit">edit user</button></p>
    </form>
    <hr>
    <div>
        <p>ชื่อรุ่น: {{user.name}}</p>
        <p>เลขรุ่น: {{user.lastname}}</p>
        <p>สเปค Projector: {{user.email}}</p>
        <p>ราคา: {{user.password}}</p>
    </div>
</div>
</template>
<script>import UsersService from '@/services/UsersService'

export default {
    data(){
        return{
            user:{
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },
    methods:{
        async editUser(){
            try{
                await UsersService.put(this.user)
                this.$router.push({
                    name: 'users'
                })

            }catch(error){
                console.log(error)
            }
        }
    }, 
    async created(){
        try{
            let userId = this.$route.params.userId
            this.user = (await UsersService.show(userId)).data
        }catch(error){
            console.log(error)
        }
    }
}
</script>
<style scoped>


</style>