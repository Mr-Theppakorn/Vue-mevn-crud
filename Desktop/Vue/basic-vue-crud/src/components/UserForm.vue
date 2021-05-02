<template>
  <div id="user-form">
    <form @submit.prevent="onSubmit">
      <label for="name">Username</label>
      <input ref="first" v-model="user.name" type="text" :class="{ 'has-error' : submitting && invalidName }" @focus="clearStatus" @keypress="clearStatus" />
      <label for="age">Age</label>
      <input v-model="user.age" type="number" :class="{ 'has-error' : submitting && invalidAge}"  @focus="clearStatus" />
      <label for="phone">Telephone number</label>
      <input v-model="user.phone" type="number" :class="{ 'has-error' : submitting && invalidPhone}"  @focus="clearStatus"  />
      <label for="email">Email</label>
      <input v-model="user.email" type="email" :class="{ 'has-error' : submitting && invalidEmail}"  @focus="clearStatus"  />
      <label for="description">Description</label>
      <input v-model="user.description" type="text" />
      <br>
      <p v-if="error && submitting" class="error-message">
        กรุณากรอกข้อมูลให้ครบ
      </p>
      <p v-if="success" class="success-message">
        เพิ่มข้อมูลสำเร็จ
      </p>
      <button class="btn">Add User</button>
    </form>
  </div>
</template>

<script>

export default {
    name: 'UserForm',
    data() {
        return {
            submitting: false,
            error: false,
            success: false,
            user: {
                name: '',
                age: '',
                phone: '',
                email: '',
                description: ''
            }
        }
    },
    methods: {
      onSubmit() {
        this.submitting = true
        this.clear()
        if ( this.invalidName|| this.invalidAge || this.invalidPhone || this.invalidEmail ) {
          this.error = true
          return
        }
        this.$emit('add:user', this.user)
        this.$refs.first.focus()
        this.user = {
                name: '',
                age: '',
                phone: '',
                email: '',
                description: ''
        }
        this.error = false
        this.submitting = false
        this.success = true
      },
      clear() {
        this.error = false
        this.success = false
      }

    },
    computed: {
        invalidName() {
          return this.user.name === ''
        },
        invalidAge() {
          return this.user.age === ''
        },
        invalidPhone() {
          return this.user.phone === ''
        },
        invalidEmail() {
          return this.user.email === ''
        }
      },
}
</script>

<style scoped>
  input, select {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  font-size: 18px;
}

.btn {
  width: 20%;
  background-color: #56ab2f;  /* fallback for old browsers */
  background-color: -webkit-linear-gradient(to right, #a8e063, #56ab2f);  /* Chrome 10-25, Safari 5.1-6 */
  background-color: linear-gradient(to right, #a8e063, #56ab2f); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  font-size: 18px;
  border-radius: 4px;
  cursor: pointer;
  transition: 0.3s all ease;
}

.btn:hover {
  background-color: green;
}

div {
  border-radius: 5px;
  background: #0575E6;  /* fallback for old browsers */
background: -webkit-linear-gradient(to right, #021B79, #0575E6);  /* Chrome 10-25, Safari 5.1-6 */
background: linear-gradient(to right, #021B79, #0575E6); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  color: white;
  padding: 20px;
  margin-bottom: 20px;
}

.error-message {
  color: crimson;
}

.success-message {
  color: green;
}
</style>
