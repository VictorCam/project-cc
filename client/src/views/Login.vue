<template>
<Navigation></Navigation>
  <div class="login">
    <h1>Login</h1>

    {{login}}

    <form @submit.prevent="onSubmit()">
      UserName:
      <br />
      <input type="text" name="username" v-model.trim="form.username" />
      <br />Password:
      <br />
      <input type="password" name="password" v-model.trim="form.password" />
      <br />
      <br />
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import { reactive } from 'vue'
import { useStore } from 'vuex'
import { useState } from '@/helpers'
import Navigation from '@/components/Navigation.vue'

export default {
  name: 'Login',
  components: {
    Navigation
  },
  setup() {
    const store = useStore()

    const jform = {username:'', password:''}
    const form = reactive({...jform}) //form login

    function onSubmit() { //method
      store.dispatch('login', form) //api call
      Object.assign(form, jform)
    }

    store.dispatch('reset') //reset to ensure data integrity
    const { login } = useState(['login']) //state api calls
    
    return { onSubmit, form, login }
  }
}
</script>