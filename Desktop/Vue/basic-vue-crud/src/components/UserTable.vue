<template>
  <div id="user-table">
    <table>
      <thead>
        <tr>
          <th>Username</th>
          <th>Age</th>
          <th>Telephone number</th>
          <th>Email</th>
          <th>Description</th>
          <th>Edit / Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td v-if="editing === user.id">
            <input type="text" v-model="user.name" />
          </td>
          <td v-else>{{ user.name }}</td>
          <td v-if="editing === user.id">
            <input type="number" v-model="user.age" />
          </td>
          <td v-else>{{ user.age }}</td>
          <td v-if="editing === user.id">
            <input type="number" v-model="user.phone" />
          </td>
          <td v-else>{{ user.phone }}</td>
          <td v-if="editing === user.id">
            <input type="email" v-model="user.email" />
          </td>
          <td v-else>{{ user.email }}</td>
          <td v-if="editing === user.id">
            <input type="text" v-model="user.description" />
          </td>
          <td v-else>{{ user.description }}</td>
          <td v-if="editing === user.id">
            <button @click="editUser(user)">Save</button>
            <button @click="cancelEdit(user)">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(user)">Edit</button>
            <button @click="$emit('delete:user', user.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
    <p v-if="users.length === 0" class="empty-table">ไม่มีข้อมูล</p>
  </div>
</template>
<script>
export default {
  name: "UserTable",
  data() {
    return {
      editing: null,
    };
  },
  methods: {
    editMode(user) {
      this.cachedUser = Object.assign({}, user)
      this.editing = user.id
    },
    editUser(user) {
      if (
        user.name === "" ||
        user.age === "" ||
        user.phone === "" ||
        user.email === ""
      )
        return;
      this.$emit("edit:user", user.id, user);
      this.editing = null
    },
    cancelEdit(user) {
        Object.assign(user, this.cacheUser)
        this.editing = null
    },
  },
  props: {
    users: Array,
  },
};
</script>

<style>
table {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100vw;
}

table td,
table th {
  border: 1px solid #ddd;
  padding: 8px;
}

table tr:nth-child(even) {
  background-color: #f2f2f2;
}

table tr:hover {
  background-color: #ddd;
}

table th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background: #f7971e; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #ffd200,
    #f7971e
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #ffd200,
    #f7971e
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  color: white;
}
button {
  background-color: #56ab2f; /* fallback for old browsers */
  background-color: -webkit-linear-gradient(
    to right,
    #a8e063,
    #56ab2f
  ); /* Chrome 10-25, Safari 5.1-6 */
  background-color: linear-gradient(
    to right,
    #a8e063,
    #56ab2f
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  color: white;
  padding: 14px 20px;
  border: none;
  font-size: 15px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.3s all ease;
  margin-left: 10px;
}

.empty-table {
  width: 100%;
  height: 100px;
  margin: 20px;
  font-size: 30px;
}
</style>
