<template>
  <div>
    <h1>Get All Users</h1>
    <div v-if="users.length">
      <div>จำนวนผู้ใช้งาน {{ users.length }}</div>
      <div v-for="user in users" v-bind:key="user.id">
            <p>id: {{ user.id }}</p>
            <p>ชื่อ-นามสกุล: {{ user.name }} - {{ user.lastname }}</p>
            <p>email: {{ user.email }}</p>
            <p>password: {{ user.password }}</p>
            <hr>
            <p><button v-on:click="navigateTo('/user/'+user.id)">ดูข้อมูลผู้ใช้</button></p>
        </div>

    </div>

    <p><button @click="navigateTo('/user/create')">สร้างผู้ใช้งาน</button></p>
  </div>
</template>

<script>
import UsersService from '../../services/UsersService'

export default {
  data() {
    return {
      users: []
    }
  },


  // Logic จะเขียนตรงนี้
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
  },

  async created() {
    try {
      this.users = (await UsersService.index()).data
      console.log(this.users)
    } catch (error) {
      console.log(error)
    }
  }
}

</script>

<style scoped>
/* CSS เฉพาะหน้านี้ */
</style>
