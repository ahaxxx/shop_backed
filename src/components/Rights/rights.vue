<template>
  <div>
    <el-breadcrumb separator="/">
      <el-breadcrumb-item><a href="/home">首页</a></el-breadcrumb-item>
      <el-breadcrumb-item>权限管理</el-breadcrumb-item>
      <el-breadcrumb-item>权限列表</el-breadcrumb-item>
    </el-breadcrumb>
    <el-card class="box-card">
      <el-table
        :data="rightsList"
        style="width: 100%"
        :border ="true"
        :stripe="true">
        <el-table-column type="index"></el-table-column>
        <el-table-column prop="authName" label="权限名称" width="180"></el-table-column>
        <el-table-column prop="path" label="路径" width="180"></el-table-column>
        <el-table-column prop="level" label="权限等级" width="180">
          <template slot-scope="scope">
            <el-tag v-if="scope.row.level === '0'" type="success">一级</el-tag>
            <el-tag v-if="scope.row.level === '1'" type="info">二级</el-tag>
            <el-tag v-if="scope.row.level === '2'" type="warning">三级</el-tag>
          </template>
        </el-table-column>
      </el-table>
    </el-card>
  </div>
</template>

<script>
export default {
  data () {
    return {
      rightsList: []
    }
  },
  created () {
    this.getRightsList()
  },
  methods: {
    async getRightsList () {
      const { data: res } = await this.$http.get('/rights/list')
      if (res.meta.status !== 200) {
        return this.$message.error('获取权限列表失败')
      }
      this.rightsList = res.data
    }
  },
  name: 'rights'
}
</script>

<style lang="less" scoped>

</style>
