<template>
  <div>
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>权限管理</el-breadcrumb-item>
      <el-breadcrumb-item>权限列表</el-breadcrumb-item>
    </el-breadcrumb>

    <!-- 卡片视图 -->
    <el-card>
      <el-table :data="rightsList" border stripe>
        <el-table-column type="index"></el-table-column>
        <el-table-column label="权限" prop="authName"></el-table-column>
        <el-table-column label="路径" prop="path"></el-table-column>
        <el-table-column label="权限等级" prop="level">
          <template v-slot="scope">
            <el-tag :type="tagLevel_[scope.row.level]">{{
              tagLevel[scope.row.level]
            }}</el-tag>
          </template>
        </el-table-column>
      </el-table>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rightsList: [],
      tagLevel: {
        0: "一级",
        1: "二级",
        2: "三级"
      },
      tagLevel_: {
        0: "",
        1: "success",
        2: "warning"
      }
    }
  },
  created() {
    this.getRightsList()
  },
  methods: {
    async getRightsList() {
      const { data: res } = await this.$http.get("rights/list")
      if (res.meta.status !== 200) {
        return this.$message.error("获取权限列表失败")
      }
      this.rightsList = res.data
    }
  }
}
</script>

<style lang="less" scoped></style>
