<template>
  <div>
    <h3>プライベートリスト</h3>
    <ul>
      <li v-for="(item, index) in list" :key="index">{{item.name}} - {{item.value}}</li>
    </ul>
    <div class="row">
      <div class="col-xs-12">
        <div class="form-group">
          <input type="text" class="form-control" v-model="name">
        </div>
        <div class="form-group">
          <input type="text" class="form-control" v-model.number="value">
        </div>
      </div>
      <div class="col-xs-12">
        <button type="button" class="btn btn-default" @click="load">Load</button>
        <button type="button" class="btn btn-default" @click="add">Add</button>
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

export default {
  name: 'vue-name',
  props: {
    uid: { type: String, default: () => '' }
  },
  components: {},
  computed: {},
  watch: {},
  data () {
    return {
      name: '',
      value: 0,
      list: []
    }
  },
  created () {
  },
  methods: {
    load () {
      const list = []
      db.collection(`users/${this.uid}/item`).get().then((snapshot) => {
        snapshot.forEach((doc) => {
          const data = doc.data()
          data.id = doc.id
          list.push(data)
        })
        this.list = list
      })
    },
    add () {
      const item = {
        name: this.name,
        value: this.value
      }
      db.collection(`users/${this.uid}/item`).add(item).then((doc) => {
        console.log('doc', doc)
      })    
    }
  }
}
</script>

<style lang="scss" scoped>

</style>