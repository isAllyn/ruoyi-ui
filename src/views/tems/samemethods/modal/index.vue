<!--
 * @Author: BORING GHOST
 * @Date: 2022-07-10 16:33:28
 * @LastEditTime: 2022-07-10 16:57:28
 * @Description: 
-->
<template>
  <div>
    <el-row>
      <el-col :xs="24" :sm="24" :md="24" :lg="24">
        <el-card shadow="hover" header="modal-keys">
          <template v-for="item in modal_names">
            <el-tooltip
              :key="item"
              :content="item || 'Top center'"
              placement="top"
            >
              <el-button
                @click="openModal(item)"
                :plain="randomBool()"
                :round="randomBool()"
                :circle="randomBool()"
                :type="randomType()"
                style="margin: 20px"
              >
                {{ item }}
              </el-button>
            </el-tooltip>
          </template>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
let last_type = "";
export default {
  name: "Methodmodal_",

  data() {
    return {};
  },
  computed: {
    modal_names() {
      return Object.keys(this.$modal) || [];
    },
  },
  mounted() {},

  methods: {
    /**
     * 开启模态框
     */
    openModal(key) {
      if (!key) return;
      if (key === "closeLoading") {
        this.$modal["loading"]("提示信息");
        return setTimeout(() => {
          this.$modal.closeLoading();
        }, 1000);
      }
      if (!this.modal_names.includes(key)) return;
      this.$modal[key]("提示信息");
      if (key === "loading") {
        setTimeout(() => {
          this.$modal.closeLoading();
        }, 1000);
      }
    },
    /**
     * 随机布尔
     */
    randomBool() {
      return Math.floor(Math.random() * (5 - 3) + 3) > 3;
    },
    /**
     *随机类型
     */
    randomType() {
      function num() {
        let value = Math.floor(Math.random() * (5 - 0) + 0);
        if (last_type === value) return num();
        last_type = value;
        return value;
      }
      return ["primary", "success", "info", "warning", "danger"][num()] || "";
    },
  },
};
</script>

<style lang="scss" scoped></style>
