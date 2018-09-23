<template>
  <div class="mb50">
    <h3>他人のリスト <small>{{targetUser.email}}</small></h3>
    <div>
      <button type="button" class="btn btn-default" @click="setUser('a')">User: a</button>
      <button type="button" class="btn btn-default" @click="setUser('r')">User: r</button>
    </div>
    <ul>
      <li v-for="(item, index) in list" :key="index">{{item.name}} - {{item.value}}</li>
    </ul>
    <div class="row">
      <div class="col-xs-12">
        <button type="button" class="btn btn-default" @click="load">Load</button>
      </div>
    </div>
  </div>
</template>

<script lang="js">
const firebase = window.firebase
const db = firebase.firestore()
db.settings({
  timestampsInSnapshots: true
})

const userObj = {
  a: { email: 'a@a.com', uid: 'akXTScIqUaUD5p8WpuHMreWOnSd2' },
  r: { email: 'reno', uid: 'v25FUZRAS7eQzWqpwv0i7igQ0zg1' }
}

export default {
  name: 'vue-name',
  components: {},
  computed: {},
  watch: {},
  data () {
    return {
      name: '',
      value: 0,
      list: [],
      targetUser: userObj.a
    }
  },
  created () {
  },
  methods: {
    load () {
      const uid = this.targetUser.uid
      const list = []
      db.collection(`users/${uid}/item`).get().then((snapshot) => {
        snapshot.forEach((doc) => {
          const data = doc.data()
          data.id = doc.id
          list.push(data)
        })
        this.list = list
      })
    },
    setUser (val) {
      this.targetUser = userObj[val]
    },
    add () {
      const item = {
        name: this.name,
        value: this.value
      }
      db.collection('open').add(item).then((doc) => {
        console.log('doc', doc)
      })    
    }
  }
}
</script>

<style lang="scss" scoped>
.mb50 {
  margin-bottom: 50px;
}
</style>