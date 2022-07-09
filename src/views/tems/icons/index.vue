<!--
 * @Author: BORING GHOST
 * @Date: 2022-07-09 17:41:51
 * @LastEditTime: 2022-07-09 18:18:20
 * @Description: 
-->
<template>
  <div>
    <el-row>
      <el-col :xs="24" :sm="24" :md="24" :lg="24">
        <el-alert :closable='false' type="warning"
                  description="svg-icon组件更改颜色是根据父组件继承而来!文档有说明!">
        </el-alert>
      </el-col>
    </el-row>
    <br />
    <!-- svg -->
    <el-row>
      <el-col :xs="24" :sm="24" :md="24" :lg="24">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span>内置的svg图标</span>
            <el-color-picker style="float:right" v-model="svg_color"
                             size="mini"></el-color-picker>
          </div>
          <template v-for="(item,index) in svg_icons">
            <el-tooltip :key="index" placement="top">
              <span style="font-size:18px"
                    slot="content">{{item.name||"名称"}}:{{item.icon}}</span>
              <el-button :style="{color:svg_color}" style="margin:10px"
                         size='small'>
                <svg-icon :icon-class="item.icon" class-name='custom-class' />
              </el-button>
            </el-tooltip>
          </template>
        </el-card>
      </el-col>
    </el-row>
    <br />
    <!-- iconfont -->
    <el-row>
      <el-col :xs="24" :sm="24" :md="24" :lg="24">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span>iconfont图标</span>
            <el-color-picker style="float:right" v-model="font_color"
                             size="mini"></el-color-picker>
          </div>
          <template v-for="(item,index) in font_icons">
            <el-tooltip :key="index" placement="top">
              <span style="font-size:18px"
                    slot="content">{{item.name||"名称"}}:{{item.icon}}</span>
              <el-button style="margin:10px" size='small'>
                <i :class="[item.icon]" :style="{color:font_color}"
                   style="font-size:30px" class="iconfont"></i>
              </el-button>
            </el-tooltip>
          </template>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import { icons, fonts } from './icon.config.js';

export default {
  name: 'SvgIconsIndex',

  data() {
    return {
      font_color: "",
      font_icons: JSON.parse(JSON.stringify(fonts) || JSON.stringify([])),
      svg_color: '',
      svg_icons: JSON.parse(JSON.stringify(icons) || JSON.stringify([]))
    };
  },

  mounted() {

  },

  methods: {

  },
};
</script>

<style lang="scss" scoped>
::v-deep .custom-class {
  font-size: 20px;
}
</style>