## 开发流程介绍

`步骤`：

1. 需求分析

2. 产品设计，语言、平台(pc、手机)、数据库(mysql、mongodb、sqlserver、redis)、功能***、产品流程(游戏规则)

3. psd  原型图(通过photoshop绘制项目假想效果)

4. UI图(绘制项目相关图片素材、图标效果)

5. 后端数据接口项目开发(数据库(表、字段)设计、服务搭建[apache、nginx、nodejs等]、开发语言[nodejs、php、python、java等])

6. 前端项目开发，根据psd和ui绘制功能页面，大量应用第3方组件库(例如elementui、vant[vue/移动端 组件库])

7. 前、后 端数据接口问题，**mock**假数据(http://mockjs.com/)、在线数据，"数据接口"可以通过yapi管理

8. **数据接口**[地址、数据] 联调  -- **禅道**(https://www.zentao.net/)管理

    

## 项目描述

针对目前大量学员在培训完之后直接去面试企业的通过率低的问题，公司研发了**黑马面面**小程序，学员在空闲时间可以通过查看企业真实面试题，也可以通过刷题寻找自己的短板进行补充，新版本提供模拟面试功能，用户可以通过微信小程序进入模拟面试模块，完成定向企业面试和自由组题模式

前端项目：

​	前台项目：微信小程序、电脑端、手机app

​	后台项目：黑马头条项目、黑马面面

后端项目：nodejs+mysql数据库开发的接口项目

​	都是API数据即可



## 安装后端项目

`步骤`：

1. 创建项目

   把hmmm-backend目录复制到指定位置

2. 把 node_modules.zip 解压到 hmmm-backend目录

   > 不要执行yarn安装依赖包，会有问题

3. 创建数据库、导入数据

   启动mysql

4. 给项目配置数据库账号(root/root)、mysql数据库名字(mianmian)

   对项目指定配置文件(**hmmm-backend/config/config.default.js**)做 数据库账号、数据库名称 配置

5. 启、停 接口项目

```
npm start
// 会同时创建许多子窗口，最小化即可 

npm stop
```

接口地址：http://127.0.0.1:7001



`注意`：

1. 后端数据接口项目启动后，有许多系统服务，不能关闭
2. 项目的上级各个目录名称不要使用"中文"或其他特殊符号，只使用英文、数字或中横线即可
3. 不要执行yarn安装全部依赖包有问题，相反复制、粘贴老师的node-modules目录做应用
4. npm start  与 stop 需要配对使用，不要重复start



## 前端项目搭建

`步骤`：

1. 复制项目代码  hmmm_frontend  到指定运行目录

2. 把 node_modules.zip文件 解压到项目根目录

   > 不要通过yarn安装全部依赖包
   >
   > 项目中使用到了node-sass依赖包，其不断升级，非常不稳定，导致yarn不能很好地安装

3. 修改config/index.js文件，配置自动开启浏览器

```
autoOpenBrowser: true
```

4. 启动项目

```
npm start
```

> 正常情况，浏览器自动开启，并可以访问到后台项目效果



`注意`：

1. 项目的上级各个目录名称不要使用"中文等特殊字符"
2. 前端项目需要后端项目服务支撑，因此启动之前请先确保后端项目(http://127.0.0.1:7001)已经开启
3. 前端项目通过Ctrl+c关闭，本身没有npm stop指令
4. 项目运行如果报static目录的问题，可以在项目根目录新建一个解决



## 前端项目目录介绍

主结构文件说明(VueCLI2)：

```bash
|-- build                          # 项目构建(webpack)相关代码
|   |-- build.js                     # 生产环境构建代码
|   |-- check-version.js             # 检查node、npm等版本
|   |-- logo.png                     # logo图片
|   |-- utils.js                     # 构建工具相关
|   |-- vue-loader.conf.js				  # vue-loader配置
|   |-- webpack.base.conf.js       # webpack基础配置
|   |-- webpack.dev.conf.js        # webpack开发环境配置
|   |-- webpack.prod.conf.js       # webpack生产环境配置
|-- config                         # 项目开发环境配置
|   |-- dev.env.js                   # 开发环境配置
|   |-- index.js                   # 项目主要配置(包括监听端口，打包路径等)
|   |-- prod.env.js                  # 生产环境配置
|-- src                              # 源码目录
|   |--api******************    # 数据接口目录
|      |-- base     # 基础接口API
|      |-- example  # 例子
|      |-- hmmm     # 功能接口API
|   |-- assets						   # 静态资源 
|   |-- components          # vue公共组件
|   |-- filters   # 过滤器
|   |-- icons     # 图标
|   |-- lang			# 多语言切换
|   |-- mixins     # 内容合并
|   |-- mock
|   |-- module-dashboard
|   |-- module-details
|   |-- module-form
|   |-- module-hmmm*******************   # 待完成的功能
|   |-- |--components # 组件
|   |-- |--pages      # 页面组件（包含8个页面） **重点**    
|   |-- |--router     # 模块路由
|   |-- |--store      # 存储数据
|   |-- module-list
|   |-- module-manage
|   |-- router**                   # vue路由
|   |-- App.vue**                  # 页面入口文件
|   |-- main.js**                  # 程序入口文件，加载各种公共组件
|-- static                     # 静态文件，比如一些图片，json数据等
|   |-- data                       # 群聊分析得到的数据用于数据可视化
|-- .babelrc                       # ES6语法编译配置
|-- .editorconfig                  # 定义代码格式
|-- .gitignore                     # git上传需要忽略的文件格式
|-- .postcssrc.js                  # post-loader的插件配置文件
|-- index.html                   # 模板文件页面
|-- package.json                   # 项目基本信息
|-- package-lock.json              # 锁定当前安装的包的依赖
|-- README.md                      # 项目说明
```

## 相关资源

- 接口文档：https://mock.boxuegu.com/project/113/interface/api[恢复版]
- 学员yapi应用：<http://yapi.demo.qunar.com/>
- 原型图：[http://czpm.itcast.cn/黑马面面/V2.0/](http://czpm.itcast.cn/%E9%BB%91%E9%A9%AC%E9%9D%A2%E9%9D%A2/V2.0/)



## 路由分析

暂时全部路由如下：

```
src\router\index.js    // main.js中直引
src\module-manage\router\index.js  // main.js中通过use()插件方式引入
src\module-hmmm\router\index.js  // main.js中通过 use()插件方式引入
```

`注意`：

​	虽然路由分为3个文件组成，系统执行的时候会把它们合并到一起



## 组件寻找

`步骤`：

​	路由==>  _import函数  ==>  src/router/import_development.js  

require().default说明：

通过require()方式(CommonJS模块化)导入 es6模块化 的默认导出内容，就必须设置default

 https://www.cnblogs.com/cangqinglang/p/10445256.html 




## 题库与数据接口结合

`步骤`：

1. 给模板绘制各个表单域  el-row/el-col/el-select
2. 组件实例声明searchForm的data成员对象，内部有各个成员(名称参考api接口)
3. 组件实例  声明普通的搜索项目成员 都是List 相关的
4. import导入相关api接口方法 1个动态的，2个常量
5. 在methods中声明方法，调用api方法获得**学科列表**数据
6. 在created中，调用methods相关方法，并把获得的数据直接赋予给组件实例普通成员
7. 在模板中对组件实例普通成员做遍历展示数据



`相关代码`：

组件文件：\hmmm-frontend\src\module-hmmm\pages\questions.vue

```js
// 把api数据接口相关方法导入进来
import { simple } from '@/api/hmmm/subjects' // 学科
// as给导入的成员设置别名
import {
  difficulty as difficultyList, 
  questionType as questionTypeList} 
  from '@/api/hmmm/constants' // 常量数据
```



组件实例的data、methods、created等成员：

```js
export default {
  name: 'QuestionsList',
  data() {
    return {
      // 定义各个搜索表单域的数据展示成员
      subjectIDList: [],
      difficultyList, // 简易成员赋值(difficultyList:difficultyList)
      questionTypeList,// 简易成员赋值

      // 定义搜索数据对象
      searchForm: {
        subjectID: '',
        difficulty: '',
        questionType: ''
      }
    }
  },
  created() {
    // 学科
    this.getSubjectIDList()
  },

  methods: {
    // 获得 学科 下拉列表数据
    async getSubjectIDList() {
      var rst = await simple()
      // console.log(rst)
      // 把获得到的学科信息赋予给 subjectIDList 成员
      this.subjectIDList = rst.data
    }
  }
}
```



模板相关代码：

```html
<template>
  <div class="dashboard-container">
    <div class="app-container">
      
      <el-row>
        <el-col :span="6">
          学科：
          <el-select v-model="searchForm.subjectID">
            <el-option v-for="item in subjectIDList" :key="item.value" :value="item.value" :label="item.label">
            </el-option>
          </el-select>
        </el-col>
        <el-col :span="6">
          难度：
          <el-select v-model="searchForm.difficulty">
            <el-option v-for="item in difficultyList" :key="item.value" :value="item.value" :label="item.label">
            </el-option>
          </el-select>
        </el-col>
        <el-col :span="6">
          试题类型：
          <el-select v-model="searchForm.questionType" style="width:140px;">
            <el-option v-for="item in questionTypeList" :key="item.value" :value="item.value" :label="item.label">
            </el-option>
          </el-select>
        </el-col>
      </el-row>
      
    </div>
  </div>
</template>
```



`注意`：

1. 学科信息 需要通过axios动态获取
2. 难度、试题类型 是常量，可以直接获取使用
3. 难度、试题类型 应用的是： es6模块化按需导入重命名 + 对象简易成员赋值



## api接口介绍

api接口分为两种类型：

1. axios动态接口数据
2. constants常量接口数据



## yapi使用

yapi是   高效、易用、功能强大  的数据接口管理平台
官网：<http://yapi.demo.qunar.com/>

简单使用：登录/注册----->导入接口api.json文件----->应用

`注意`：

​	yapi首次注册登录是通过”用户名“，后期要使用“邮箱账号“登录



## 分配任务

`步骤`：

1. git远程仓库：	http://github.com

2. 组长

   1. 创建远程仓库

   2. 拉取成员进入仓库????

   3. 上传本地代码(hmmm_frontend)到远程仓库(默认是master分支)

      部署hmmm_frontend

      git init  // 注意，如果当前项目没有git版本库，请先初始化(git init)

      git add .

      git commit -m '提交日志'

      git push 远程仓库地址   分支(master)

      

   4. 创建新git分支并切换进入( git checkout -b xxx )，与普通成员一样做具体业务功能开发

      > git  remote add 别名  远程仓库地址   // 给远程仓库设置访问别名

   

3. 普通成员

   1. git  clone 复制远程仓库内容到本地（git clone https仓库地址）

   2. 创建自己的开发分支(可以使用自己的名字拼音)并切换进入 (git checkout -b xxx )

   3. 在自己的分支里边做开发中。。。  

   4. add/commit/push 推送**自己的分支**到远程仓库

      > 普通组员关于远程仓库地址有一个默认别名：  *origin* 



在自己的分支上开发各自分配的功能

- 基础题库
- 精选题库
- 试题审核
- 组题列表
- 学科管理
- 目录管理
- 标签管理
- 面试技巧
