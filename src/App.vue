<template>
  <div id="app" class="mt30">
    <div class="container">
      <div class="row">
        <div class="col-xs-12">
          isLogin: {{ isLogin }}, email: {{ email }}, uid: {{ uid }}
        </div>
      </div>
      <div class="row">
        <div class="col-xs-6">
          <AuthBox></AuthBox>
        </div>
        <div class="col-xs-6">
          <LoginBox></LoginBox>
        </div>
      </div>
      <hr>
      <div class="row">
        <div class="col-xs-6">
          <AddItem :uid="uid"></AddItem>
        </div>
        <div class="col-xs-6">
          <AddOpenList :uid="uid"></AddOpenList>
        </div>
      </div>
      <hr>
      <div class="row">
        <div class="col-xs-12">
          <OtherUserList></OtherUserList>
        </div>
      </div>
    </div>
    
  </div>
</template>

<script lang="js">
import AuthBox from './components/AuthBox.vue'
import LoginBox from './components/LoginBox.vue'
import AddItem from './components/AddItem.vue'
import AddOpenList from './components/AddOpenList.vue'
import OtherUserList from './components/OtherUserList.vue'
const firebase = window.firebase
const db = firebase.firestore()

export default {
  name: 'vue-name',
  components: {
    AuthBox,
    LoginBox,
    AddItem,
    AddOpenList,
    OtherUserList
  },
  computed: {},
  watch: {},
  data () {
    return {
      email: '',
      uid: '',
      isLogin: false
    }
  },
  created () {
    firebase.auth().onAuthStateChanged((user) => {
      // console.log('has user?', user)
      if (user) {
        this.isLogin = true
        this.email = user.email
        this.uid = user.uid
      } else {
        this.isLogin = false
        this.email = ''
      }
    })
  },
  methods: {
  }
}
</script>

<style lang="scss">
.mt30 {
  margin-top: 30px;
}
</style>
