<template>
  <el-row :gutter="20">
    <el-col :span="6" v-for="user in users" :key="user.id">
      <el-card class="card" v-loading="loading">
        <el-image
          :src="user.avatar_url"
          fit="cover"
        >
        </el-image>
        <div style="padding: 8px;">
          <div class="bottom clearfix">
            <el-link :underline="false" :href="user.html_url" type="info">{{user.login}}</el-link>
          </div>
        </div>
      </el-card>
    </el-col>

  </el-row>
</template>

<script>
export default {
  name:'List',
  data() {
    return {
      users: [],
      loading: true
    }
  },
  mounted () {
    this.$bus.$on('updateUser', (data) => {
      if (data === null) {
        this.$message('loading')
      }
      else {
        this.users = data
        this.loading = false
      }
    })
  },
  beforeDestroy() {
    this.$bus.$off('updateUser')
  }
}
</script>

<style scoped>
  .card {
    text-align: center;
    font-size: 10px;
    font-weight: light;
  }

  .image {
    width: 100%;
  }
</style>