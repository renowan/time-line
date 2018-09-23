<template>
  <div>
    <div class="row">
      <div class="col-xs-12">
        <h3>Login</h3>
      </div>
      <div class="col-xs-12">
        <div class="form-group">
          <input type="text" class="form-control" v-model="email">
        </div>
      </div>
      <div class="col-xs-12">
        <div class="form-group">
          <input type="text" class="form-control" v-model="password">
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-12">
        <button class="btn btn-default" type="button" @click="add">sign in</button> 
        <button class="btn btn-default" type="button" @click="reset">reset</button>
        <button class="btn btn-default" type="button" @click="loginout">Login Out</button>
      </div>
    </div>
  </div>
</template>

<script lang="js">
export default {
  name: 'vue-name',
  components: {},
  computed: {},
  watch: {},
  data () {
    return {
      email: '',
      password: '',
    }
  },
  created () {},
  methods: {
    add () {
      const { email, password } = this
      firebase.auth().signInWithEmailAndPassword(email, password).then((result) => {
        console.log('signIn', result)
      }).catch((error) => {
        console.log('add user error', error)
      });
    },
    reset () {

    },
    loginout () {
      firebase.auth().signOut().then((result) => {
      })
    }
  }
}
</script>

<style lang="scss" scoped>
</style>