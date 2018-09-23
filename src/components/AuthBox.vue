<template>
  <div>
    <div class="row">
      <div class="col-xs-12">
        <h3>Add User
        </h3>
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
            <button type="button" class="btn btn-default" @click="add">Add</button>
            <button type="button" class="btn btn-default" @click="reset">reset</button>
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
      firebase.auth().createUserWithEmailAndPassword(email, password).then((result) => {
        console.log('add user', result)
      }).catch((error) => {
        console.log('add user error', error)
      });
    },
    reset () {

    }
  }
}
</script>

<style lang="scss" scoped>

</style>