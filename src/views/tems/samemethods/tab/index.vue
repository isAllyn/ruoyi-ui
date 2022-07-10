<!--
 * @Author: BORING GHOST
 * @Date: 2022-07-10 15:28:12
 * @LastEditTime: 2022-07-10 16:24:20
 * @Description: 
-->
<template>
  <div>
    <el-row>
      <el-col :xs="24" :sm="24" :md="24" :lg="24">
        <el-card shadow="hover" header="当前的标签">
          <template v-if="tag_views.length > 0">
            <el-table :data="tag_views" style="width: 100%">
              <el-table-column type="index" width="50" />
              <el-table-column prop="title" label="Title"> </el-table-column>
              <el-table-column prop="name" label="Name"> </el-table-column>
              <el-table-column prop="path" label="Path"> </el-table-column>
              <el-table-column fixed="right" label="操作">
                <template slot-scope="scope">
                  <el-button
                    @click="openPage(scope.row)"
                    style="margin: 5px"
                    size="mini"
                  >
                    跳转
                  </el-button>
                  <el-button
                    @click="updatePage(scope.row)"
                    style="margin: 5px"
                    size="mini"
                    type="success"
                    plain
                  >
                    修改
                  </el-button>
                  <el-button
                    @click="closePage(scope.row)"
                    style="margin: 5px"
                    size="mini"
                    type="danger"
                    plain
                  >
                    关闭
                  </el-button>
                </template>
              </el-table-column>
            </el-table>
          </template>
          <el-empty :image-size="40" v-else></el-empty>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: "SameMethodsTab",

  data() {
    return {};
  },
  computed: {
    tag_views() {
      return this.$store.getters.visitedViews;
    },
  },
  mounted() {},

  methods: {
    /**
     * 关闭
     */
    closePage(row) {
      if (this.tag_views.length <= 1) return this.$modal.msg("禁止全部关闭");
      // 关闭指定页签
      const obj = { path: row.path, name: row.name };
      this.$tab.closePage(obj).then(() => {
        this.$modal.msgSuccess("关闭成功");
      });
    },
    /**
     * 修改页签
     */
    updatePage(row) {
      let title = window.prompt("修改后的标题?");
      if (!title) return;
      title = title.trim();
      let route = this.tag_views.find((v) => v.meta.title === row.title);
      if (!route) return this.$modal.msg("标签查找失败");
      const obj = Object.assign({}, route, { title });
      this.$tab.updatePage(obj);
      this.$tab.updatePage(obj).then(() => {
        this.$modal.msgSuccess("修改成功");
      });
    },
    /**
     * 开启页签
     */
    openPage(row) {
      if (row.hasOwnProperty("path") || row.hasOwnProperty("title")) {
        if (row["title"] === this.$route.meta.title)
          return this.$modal.msg("本页");
        this.$tab.openPage(row.title, row.path).then(() => {
          this.$modal.msgSuccess("开启成功");
        });
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
