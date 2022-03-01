<template>
  <div>
    <el-row :gutter="20">
      <el-col :span="8">
        <el-input
          placeholder="Please input the username that you want to search"
          v-model="keyWord"
          :style="{width: '92%'}"
          clearable
          @keyup.enter.native="getUsers"
        >
          <el-button slot="append" icon="el-icon-search" @click="getUsers"></el-button>
        </el-input>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Search',
  data() {
    return {
      keyWord: ''
    }
  },
  
  methods: {
    getUsers() {
      axios.get('https://api.github.com/search/users?q=' + this.keyWord).then(
        res => {
          // console.log(res.data.items)
          const items = JSON.stringify(res.data.items)
          localStorage.setItem('items', items)
          if (localStorage.getItem('items') != null) {
            const res = localStorage.getItem('items')
            this.$bus.$emit('updateUser', JSON.parse(res))
          }
        }
      )
    }/* ,

    getUsername() {
      const items = JSON.parse(localStorage.getItem('items'))
      this.$bus.$emit('updateUser', items)
    } */
  }
}
</script>

<style>
  
</style>