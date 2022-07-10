<!--
 * @Author: BORING GHOST
 * @Date: 2022-07-10 14:25:30
 * @LastEditTime: 2022-07-10 15:25:46
 * @Description: 
-->
<template>
  <div>
    <!-- 所有的字典类型 -->
    <el-row>
      <el-col :xs="24" :sm="24" :md="24" :lg="24">
        <el-skeleton :loading="typeLoading" animated>
          <template slot="template">
            <el-skeleton-item style="height: 100px" variant="text" />
          </template>
          <el-card shadow="nerver" header="所有的字典类型">
            <template v-if="dict_types.length > 0">
              <template v-for="item in dict_types">
                <el-tooltip
                  :key="item.dictCode"
                  :content="item.dictLabel || 'Top center'"
                  placement="top"
                >
                  <el-tag
                    @click="getDictItemInfo(item.dictType)"
                    :type="randomType()"
                    style="margin: 5px; cursor: default"
                  >
                    {{ item.dictType || "加载失败" }}
                  </el-tag>
                </el-tooltip>
              </template>
            </template>
            <el-empty :image-size="50" v-else>
              <el-button @click="getDictTypeList" type="text">
                重新加载
              </el-button>
            </el-empty>
          </el-card>
        </el-skeleton>
      </el-col>
    </el-row>
    <br />
    <!-- 单个字典类型的数据 -->
    <el-row>
      <el-col :xs="24" :sm="24" :md="24" :lg="24">
        <el-skeleton :loading="dictItemLoading" animated>
          <template slot="template">
            <el-skeleton-item style="height: 100px" variant="text" />
          </template>
          <el-card shadow="nerver" header="单个类型的数据">
            <template v-if="dict_itemInfo">
              <Editor v-model="dict_itemInfo" :readOnly="true"></Editor>
            </template>
            <el-empty :image-size="50" v-else></el-empty>
          </el-card>
        </el-skeleton>
      </el-col>
    </el-row>
  </div>
</template>

<script>
/* api */
import { listData, getDicts } from "@/api/system/dict/data.js";

let current_type = 0;

export default {
  name: "Temsdicts",

  data() {
    return {
      typeLoading: false,
      dict_types: [],
      dictItemLoading: false,
      dict_itemInfo: "",
    };
  },
  created() {
    this.loadData();
  },

  methods: {
    loadData() {
      this.getDictTypeList();
    },
    /**
     * 查询单个字典类型的数据
     */
    async getDictItemInfo(dictType) {
      try {
        this.dictItemLoading = true;
        if (!dictType) return new Error("没有类型值");
        let { data } = await getDicts(dictType);
        this.dict_itemInfo = JSON.stringify(data);
      } catch (e) {
        console.log(e);
      } finally {
        this.dictItemLoading = false;
      }
    },
    /**
     * 字典所有类型
     */
    async getDictTypeList() {
      try {
        this.typeLoading = true;
        let { rows } = await listData();
        this.dict_types = rows;
      } catch (e) {
        console.log(e);
      } finally {
        this.typeLoading = false;
      }
    },
    /**
     * tag随机状态
     */
    randomType() {
      console.log(1);
      function num() {
        let value = Math.floor(Math.random() * (5 - 0) + 0);
        if (value === current_type) return num();
        current_type = value;
        return value;
      }
      return ["success", "info", "warning", "danger"][num()] || "";
    },
  },
};
</script>

<style lang="scss" scoped></style>
