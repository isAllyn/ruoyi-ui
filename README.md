## 开发

```bash
# 克隆项目
git clone https://gitee.com/y_project/RuoYi-Vue

# 进入项目目录
cd ruoyi-ui

# 安装依赖
npm install

# 建议不要直接使用 cnpm 安装依赖，会有各种诡异的 bug。可以通过如下操作解决 npm 下载速度慢的问题
npm install --registry=https://registry.npmmirror.com

# 启动服务
npm run dev
```

浏览器访问 http://localhost:80

## 发布

```bash
# 构建测试环境
npm run build:stage

# 构建生产环境
npm run build:prod
```

## 使用

### 菜单

搭建 4 级菜单

1. 菜单管理处进行配置
2. 搭建响应的文件
3. 2 级以上的菜单都要选择目录

### 字典

```
使用字典可以直接通过dicts属性导入即可用dict.type.字典类型使用,文档有示例
例外api处有查询字典列表的接口
listData 查询字典列表
getDicts 根据字典类型查询该类型的数据
```

### 通用方法

1. tab

```
标签的增删改跟,单个页面的刷新
```

2. modal

```
各类模态框
```
