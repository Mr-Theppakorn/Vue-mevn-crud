<template>
  <div id="app" class="container">
    <h1>Data User</h1>
    <UserForm @add:user="addUser" />
    <UserTable :users="users" @delete:user="deleteUser" @edit:user="editUser" />
  </div>
</template>

<script>
import UserForm from '@/components/UserForm'
import UserTable from '@/components/UserTable'

export default {
  name: 'App',
  components: {
    UserForm,
    UserTable
  },
  data() {
    return {
      users: [{
        id: 1,
        name: 'Theppakorn Pongteedee',
        age: 24,
        phone: 1123456789,
        email: 'Theppakorn@gmail.com',
        description: 'ReactJS and VueJs'
      }]
    }
  },
  methods: {
    addUser(user) {
      const Id = this.users.length > 0 ? this.users[this.users.length-1].id : 0;
      const id = Id +1;
      const newUser = {...user, id} 
      this.users = [...this.users, newUser]
      console.log(this.users)
    },
    deleteUser(id) {
      this.users = this.users.filter(user => user.id !== id)
    },
    editUser(id, updatedUser) {
      this.user = this.users.map(user => user.id === id ? updatedUser : user)

    }

    
  },

}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  h1 {
    margin: 8px;
  }

</style>
