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



5. git常用操作

   ```bash
   git add .
   git commit -m 'xxx'
   git clone 远程仓库地址	 // 同一个项目执行一次
   git remote add 别名  远程仓库地址  // 给远程仓库设置访问别名
   git pull 远程仓库地址/别名 远程分支名<:本地分支名>  // 更新， 同一个项目频繁执行
   git push 远程仓库地址/别名  分支  // 给远程仓库进行推送
   ```
   
8. vue全家桶

   VueCli  +  vue-router + Vuex + axios + devtools +组件库(element-ui) 等与vue有关系的技术的统称



## 基础题库搜索框

`步骤`：

1. 绘制相关的el-row   el-col  el-select/el-option   el-input

   ```html
   <el-card class="box-card">
     <el-row>
       ……
       <el-col :span="6">标签:
         <el-select placeholder="请选择" v-model="searchForm.tags" style="width:135px">
         </el-select>
       </el-col>
     </el-row>
   
     <el-row :gutter="10">
       <el-col :span="6">城市：
         <el-select placeholder="请选择" v-model="searchForm.province" style="width:102px">
         </el-select>
         <el-select placeholder="请选择" v-model="searchForm.city" style="width:102px">
         </el-select>
   
       </el-col>
       <el-col :span="6">关键字：
         <el-input type="text" placeholder="请输入关键字" 
                   v-model="searchForm.keyword" style="width:160px"></el-input>
       </el-col>
       <el-col :span="6">题目备注：
         <el-input type="text" placeholder="请输入备注" 
                   v-model="searchForm.remarks" style="width:160px"></el-input>
       </el-col>
       <el-col :span="6">企业简称：
         <el-input type="text" placeholder="请输入简称" 
                   v-model="searchForm.shortName" style="width:150px"></el-input>
       </el-col>
     </el-row>
   
     <el-row :gutter="10">
       <el-col :span="6">方向：
         <el-select placeholder="请选择" v-model="searchForm.direction" style="width:135px">
         </el-select>
       </el-col>
       <el-col :span="6">录入人：
         <el-select placeholder="请选择" v-model="searchForm.creatorID" style="width:135px">
         </el-select>
       </el-col>
       <el-col :span="6">二级目录：
         <el-select placeholder="请选择" v-model="searchForm.catalogID" style="width:135px">
         </el-select>
       </el-col>
       <el-col :span="6">
         <el-button size="mini">清除</el-button>
         <el-button type="primary" size="mini">搜索</el-button>
       </el-col>
     </el-row>
   </el-card>
   ```

   

2. 绘制相关的组件实例data的searchForm的各个成员

   ```js
         // 搜索表单数据对象
         searchForm: {
           subjectID: '', // 科学
           difficulty: '', // 难度
           questionType: '', // 试题类型
           tags: '', // 标签
           province: '', // 省份
           city: '', // 城市
           keyword: '', // 关键字
           remarks: '', // 备注
           shortname: '', // 企业简称
           direction: '', // 方向
           creatorID: '', // 录入人
           catalogID: '' // 二级目录
         }
   ```



## 标签下拉列表

1. 制作data成员tagsList

   ```js
   tagsList: [], // 标签
   ```

2. import导入获取标签数据 的simple(tagsSimple)方法

   ```js
   import {simple as tagsSimple} from '@/api/hmmm/tags' // 获取标签信息方法导入
   ```

3. 给methods声明getTagsList()方法，调用tagsSimple获得标签数据，并赋予给tagsList

   ```js
   // 获得 标签 列表数据
   async getTagsList() {
     var rst = await tagsSimple() // Promise对象 变为 dt了
     this.tagsList = rst.data
   },
   ```

4. 在created中调用getTagsList方法

   ```js
   created(){
     // 获得标签信息
     this.getTagsList()
   }
   ```

5. 模板中通过el-option把tagsList数据信息以下拉列表形式展示出来

   ```html
   <el-option 
              v-for="item in tagsList" 
              :key="item.value" 
              :label="item.label" 
              :value="item.value">
   </el-option>
   ```


`注意`：

​	各个表单域(下拉列表/输入框/文本域)标签需要设置**v-model**属性，避免不能设置信息



## 录入人下拉列表

`步骤`：

1. 制作data成员creatorIDList

   ```js
   creatorIDList: [], // 录入人
   ```
   

   
2. import导入获取标签数据 的simple(usersSimple)方法(api/base/users.js)

   ```js
   import {simple as usersSimple} from '@/api/base/users' // 获取录入人信息方法导入
   ```
   

   
3. 给methods声明getCreatorIDList()方法，调用usersSimple获得标签数据，并赋予给creatorIDList

   ```js
   // 获得 录入人 列表数据
   async getCreatorIDList() {
     var rst = await usersSimple()
     this.creatorIDList = rst.data
   },
   ```
   

   
4. 在created中调用getcreatorIDList方法

   ```js
   created(){
     // 获得录入人信息
     this.getCreatorIDList()
   }
   ```
   

   
5. 模板中通过el-option把creatorIDsList数据信息以下拉列表形式展示出来

   ```html
   <el-option 
              v-for="item in creatorIDList" 
              :key="item.id" 
              :label="item.username" 
              :value="item.id">
   </el-option>
   ```
   

`注意`：

1. 录入人的返回信息是**id**和**username**字段，不同于其他项目是value/label
2. 录入人的名称，在api程序接口里边为users，在yapi数据接口里边称为creatorID



## 二级目录下拉列表

`步骤`：

1. 制作data成员catalogIDList

   ```js
   catalogIDList: [], // 二级目录
   ```
   

   
2. import导入获取标签数据 的simple(directorysSimple)方法(api/hmmm/directorys.js)

   ```js
   import{simple as directorysSimple}from '@/api/hmmm/directorys' // 获取二级目录信息方法导入
   ```
   

   
3. 给methods声明getCatalogIDList()方法，调用directorysSimple获得标签数据，并赋予给catalogIDList

   ```js
   // 获得 录入人 列表数据
   async getCatalogIDList() {
     var rst = await directorysSimple()
     this.catalogIDList = rst.data
   },
   ```
   

   
4. 在created中调用getCatalogIDList方法

   ```js
   created(){
     // 获得 二级目录 信息
     this.getCatalogIDList()
   }
   ```
   

   
5. 模板中通过el-option把catalogIDList数据信息以下拉列表形式展示出来

   ```html
   <el-option 
              v-for="item in catalogIDList" 
              :key="item.value" 
              :label="item.label" 
              :value="item.value">
   </el-option>
   ```



`注意`：

​	二级目录的名称，在api程序接口里边为directorys，在yapi数据接口里边称为catalogID




## 方向下拉列表

`步骤`：

1. import导入方向数据，并起别名 {direction as directionList}  (api/hmmm/drection.js)

   ```js
   import { direction as directionList } from '@/api/hmmm/constants'
   ```
   
2. data中给做**简易成员赋值**方式制作directionList

   ```js
   directionList, // 方向
   ```
   
3. 模板中el-option遍历展示 directionList

   ```html
   <el-option 
              v-for="item in directionList" 
              :key="item" 
              :value="item" 
              :label="item">
   </el-option>
   ```



`注意`：

​	方向信息就是一个**普通数组**，直接对应item做应用即可	



## 城市

`步骤`：

1. import引入 citys.js的两个方法 provinces/citys 两个方法

   ```js
   import {provinces, citys} from '@/api/hmmm/citys' // 获取 省份/城市 信息方法导入
   ```
   

   
2. 在methods中，简易成员赋值声明 provinces 方法

   ```js
   // 获得 省份 信息，简易成员赋值
   provinces, // provinces:provinces
   ```
   

   
3. 模板中 el-option 直接对 provinces方法做遍历，设置下拉列表信息

   ```html
   <el-option 
             v-for="item in provinces()" 
             :key="item" 
             :label="item" 
             :value="item">
   </el-option>
   ```
   


`注意`：

​	v-for遍历，既可以遍历data成员，也可以遍历methods方法，但是要给方法后边设置() 括号



## 区县

`步骤`：

1. 设置data成员 cityList

   ```js
   cityList: [], // 区县信息
   ```
   

   
2. 给**城市**设置change内容改变事件  @change="getCitys"

   ```html
   <el-select @change="getCitys(searchForm.province)" v-model="searchForm.province">
   ```
   

   
3. 在methods中，设置getCitys(pname代表当前选中省份)方法，调用citys()获取对应的城市信息并赋予给cityList

   ```js
   // 获得 城市 信息
   // 这个pname形参就代表被选中的省份信息
   getCitys(pname) {
     this.searchForm.city = '' // 清除之前选取好的城市
     this.cityList = citys(pname)
   },
   ```
   

   
4. 模板中遍历cityList展示省份对应的城市信息

   ```html
   <el-option 
              v-for="item in cityList" 
              :key="item" 
              :label="item" 
              :value="item">
   </el-option>
   ```



## 基础题库数据列表

`步骤`：

1. 制作data成员questionList

   ```js
   questionsList: [], // 基础题库列表信息
   ```
   

   
2. import导入list方法(api/hmmm/questions.js)

   ```js
   import {list} from '@/api/hmmm/questions' // 基础题库相关api导入
   ```
   

   
3. 制作methods方法getQuesionList()，调用api接口list，获得题库列表数据赋予给 questionList成员

   ```js
   // 获得基础题库列表信息
   async getQuestionsList() {
     var rst = await list()
     // 把获得好的题库列表信息赋予给 questionList 成员
     this.questionsList = rst.data.items
   },
   ```
   

   
4. created中调用   getQuesionsList()

   ```js
   created(){
     // 获得 基础题库 列表信息
     this.getQuestionsList()
   }
   ```
   

   
5. 绘制el-table/el-table-column 展示各个试题信息

   ```html
   <el-table :data="questionsList" style="width:100%">
     <el-table-column label="序号" type="index"></el-table-column>
     <el-table-column label="试题编号" prop="number"></el-table-column>
     <el-table-column label="学科" prop="subject"></el-table-column>
     <el-table-column label="题型" prop="questionType"></el-table-column>
     <el-table-column label="题干" prop="question"></el-table-column>
     <el-table-column label="录入时间" prop="addDate" width="170"></el-table-column>
     <el-table-column label="难度" prop="difficulty" ></el-table-column>
     <el-table-column label="录入人" prop="creator"></el-table-column>
     <el-table-column label="操作" width="200">
       <template slot-scope="stData">
         <a href="#">预览</a>
         <a href="#">修改</a>
         <a href="#">删除</a>
         <a href="#">加入精选</a>
       </template>
     </el-table-column>
   </el-table>
   ```



6. 调整样式

   给el-row和el-table设置样式

   ```html
   <style scoped>
   .el-row {
     margin-bottom: 10px;
   }
   .el-table {
     margin-top: 20px;
   }
   </style>
   ```
   



## 题型数字转汉字

`步骤`：

0. 把mysql中“题型hm_questions表的questionType字段”信息都更改为数字的 1/2/3

1. 给题型 el-table-column设置 :formatter属性

   ```html
   <el-table-column label="题型" :formatter="questionTypeFMT" ></el-table-column>
   ```
   

   
2. 在methods方法中生成 formatter对应的方法，实现当前列内容的转化操作

   ```js
   // 对"题型"数据进行二次修饰
   // row: 代表每条记录信息(stData.row.xx)
   // column: 代表列的信息(一般不使用)
   // cellValue: 当前正在处理的目标列的内容(与row.questionType一致)
   // index: 0/1/2.. 序号信息
   questionTypeFMT(row, column, cellValue, index) {
     // console.log(index)
     // return 返回的信息会去覆盖当前的column列的内容
     return this.questionTypeList[cellValue - 1].label
   },
   ```

`注意`：

​	el-table-column组件可以通过  **formatter**  属性对当前列的信息做格式转换等修饰操作



## 难度数字转汉字

`步骤`：

0. 把mysql中“难度hm_questions 的difficulty字段”信息都更改为数字的 1/2/3

1. 给题型 el-table-column设置 :formatter属性

   ```html
   <el-table-column label="难度" prop="difficulty"  :formatter="difficultyFMT">
   ```
   

   
2. 在methods方法中生成 formatter对应的方法，实现当前列内容的转化操作

   ```js
   // 难度数字转汉字
   difficultyFMT(row, column, cellValue) {
     return this.difficultyList[cellValue - 1]['label']
   },
   ```



## 时间格式化

`实现`：

通过**作用域插槽**方式获取每行的时间信息，并结合过滤器做信息格式转变

```html
<el-table-column label="录入时间" width="170">
  <!--table表格column中获取数据信息，要使用 作用域插槽 形式-->
  <span slot-scope="stData">{{stData.row.addDate | parseTimeByString}}</span>
</el-table-column>
```

`注意`：

​	时间变为格式化样子，可以通过**:formatter**实现，但是需要额外编辑methods方法，**过滤器**已经封装好直接使用更方便



## 搜索数据

`步骤`：

1. 制作watch监听器，对searchForm表单对象进行深度监听，发现搜索表单数据由变化，就重新获得试题列表信息

   ```js
   watch: {
     searchForm: {
       handler: function(newV, oldV) {
         // 重新获得试题
         this.getQuestionsList()
       },
       deep: true
     }
   },
   ```
   
2. 在获得试题列表的methods方法中，设置searchForm参数，作为获得试题列表信息的筛选条件

   ```js
   async getQuestionsList() {
     // 给list传递数据检索的条件信息
     var rst = await list(this.searchForm)
     this.questionsList = rst.data.items
   }
   ```


`注意`：

​	目前只有**关键字**(题干)一个项目支持搜索，其他的都是摆设



## 题库删除

`步骤`：

1. 给删除按钮设置@click.prevent="del(stData.row)" 单击事件

   ```html
   <!--如下超链接a标签单击后，click和href都执行了
   我们需要只执行click，不要执行href
   处理：使用事件修饰符
   @click.prevent: 只执行事件，标签的默认动作不走
   // prevent:阻止浏览器默认动作(a有动作、form表单有动作)
   
   @click.native: 使得事件直接作用到组件的html标签身上
   -->
   <a href="#" @click.prevent="del(stData.row)">删除</a>
   ```
   
> prevent：阻止a标签默认跳转执行

2. import引入remove接口方法， api/hmmm/questions.js

   ```js
   import { list, remove } from '@/api/hmmm/questions' // 基础题库相关api导入
   ```
   

   
3. 在methods中制作del方法，实现数据参数操作

   ```js
   // 删除题库
   del(question) {
     this.$confirm('确认要删除此试题么?', '删除', {
       confirmButtonText: '确定',
       cancelButtonText: '取消',
       type: 'warning'
     }).then(async () => {
       // await:保证数据删除完毕，再做刷新
       await remove(question)
       // 页面刷新
       this.getQuestionsList()
     }).catch(() => { })
   },
   ```
   


`注意`：

1. 要把被删除的"**整个**"记录对象当做参数传递使用(非id)
2. @click.prevent 设置**事件修饰符**，阻止浏览器默认动作 （即阻止a标签超链接动作）
3. asycn和await保障数据删除完毕，再做更新



## 插件

​	通过独立的模块把“Vue实例”的各个成员给设置好，待需要使用之时，快速配置部署，这个模块就是“插件”

官网：[https://vue.docschina.org/v2/guide/plugins.html#%E7%BC%96%E5%86%99%E6%8F%92%E4%BB%B6](https://vue.docschina.org/v2/guide/plugins.html#编写插件)

​	各个插件都可以给Vue声明许多成员，形成独立模块，需要的时候就引入使用，方便程序的开发、维护	



声明插件

```js
// MyPlugin.js
export default {
  install(obj){
    obj.prototype.xx = yy  // 声明全局属性，类似data
    obj.prototype.$xx = ()=>{}  // 声明全局方法，类似methods
    obj.filter('timeFT',function(origin){ }) // 声明全局过滤器
    obj.component(xx,yy)  // 声明全局组件
    obj.directive(xx,yy)  // 声明全局指令
    ……
  }
}
```

> obj 是自定义名字，代表 "Vue 构造函数" 
>
> 可以通过插件完成 data、methods、directive、filter、component等全局成员的声明



使用插件

```js
import MyPlugin from './MyPlugin'
Vue.use(MyPlugin)    // 本质：MyPlugin.install(Vue)
或 
Vue.use(MyPlugin, { someOption: true })

new Vue({
  // ...组件选项
})
```

> 使用插件需要在 new  Vue()之前

应用：

创建插件src/MyPlugin.js

```js
// 声明一个插件，内部有两个组件(分页、表格)
export default {
  // 对象有名称为install的成员，是方法，install是固定的，不能该
  // obj:固定代表"Vue对象"
  install: function(obj) {
    // 普通组件声明
    obj.component('it-table', {
      template: `
        <table>
          <tr><td>序号</td><td>名称</td></tr>
          <tr><td>1001</td><td>奔驰</td></tr>
          <tr><td>1002</td><td>宝马</td></tr>
        </table>
      `
    })
    obj.component('it-page', {
      template: `
        <ul>
          <li>1</li>
          <li>2</li>
          <li>3</li>
        </ul>
      `
    })
  }
}
```

main.js中引入、注册插件：

```js
// 自定义插件引入和使用
import mypu from '@/MyPlugin.js'
Vue.use(mypu) // 本质是内部的install方法得到执行了
```

具体组件中使用插件提供的组件：

```html
<it-table></it-table>
<it-page></it-page>
```



# 题库数据增加

## 设置新增按钮

给 试题列表 设置 “新增”和 “批量导入”按钮

制作相关按钮

```html
<el-row>
  <el-col>
    <el-button type="primary" size="mini" @click="$router.push('/questions/new')">
      新增试题
    </el-button>
    <el-button type="danger" size="mini">
      批量导入
    </el-button>
  </el-col>
</el-row>
```



## 绘制简单表单域元素

`目标`：

​	添加题库 绘制简单(学科、目录、企业、城市、方向)表单域元素  和  相关data成员

`步骤`：

1. 绘制相关的el-form   el-select

   > 在src/module-hmmm/pages/questions-new.vue中设置

   ```html
   <el-card class="box-card">
     <el-form ref="addFormRef" :model="addForm" label-width="120px">
       <!--:model作用：可以使得el-form针对表单的全部信息进行收集，固定属性-->
       <el-form-item label="学科：">
         <el-select v-model="addForm.subjectID">
         </el-select>
       </el-form-item>
       <el-form-item label="目录：">
         <el-select v-model="addForm.catalogID">
         </el-select>
       </el-form-item>
       <el-form-item label="企业：">
         <el-select v-model="addForm.enterpriseID">
         </el-select>
       </el-form-item>
       <el-form-item label="城市：">
         <el-select v-model="addForm.province" @change="getCitys(addForm.province)">
         </el-select>
         <el-select v-model="addForm.city">
         </el-select>
       </el-form-item>
       <el-form-item label="方向：">
         <el-select v-model="addForm.direction">
         </el-select>
       </el-form-item>
     </el-form>
   </el-card>
   ```

   

2. 制作组件实例data的addForm的各个成员

   ```js
   // 添加试题 表单数据对象
   addForm: {
     subjectID: '', // 学科
     catalogID: '', // 二级目录
     enterpriseID: '', // 企业
     city: '', // 区县
     province: '', // 城市
     direction: '', // 方向
   }
   ```



## 学科、目录、城市、方向表单域绘制

1. 制作data成员

   ```js
   subjectIDList: [], // 学科
   catalogIDList: [], // 二级目录
   cityList: [], // 区县信息
   directionList, // 方向(简易成员赋值)
   ```
   
2. import导入获取标签数据 的simple(别名subjectsSimple)方法

   ```js
   import { simple as subjectsSimple } from '@/api/hmmm/subjects' // 学科
   import { simple as directorysSimple } from '@/api/hmmm/directorys' // 二级目录
   import { provinces, citys } from '@/api/hmmm/citys' // 城市和区县
   // 常量(方向)
   import { direction as directionList } from '@/api/hmmm/constants'
   ```
   
3. 给methods声明getSubjectIDList()方法，调用subjectsSimple获得标签数据，并赋予给subjectIDList

   ```js
   provinces, // 获得城市的方法(简易成员赋值)
   // 学科 列表信息
   async getSubjectIDList() {
     var rst = await subjectsSimple()
     this.subjectIDList = rst.data
   },
   // 目录 列表信息
   async getCatalogIDList() {
     var rst = await directorysSimple()
     this.catalogIDList = rst.data
   },
   // 获得 区县 信息
   // 这个pname形参就代表被选中的省份信息
   getCitys(pname) {
     this.addForm.city = '' // 清除之前选取好的城市
     this.cityList = citys(pname)
   }
   ```
   
4. 在created中调用getSubjectIDList方法

   ```js
   created() {
     this.getSubjectIDList() // 学科
     this.getCatalogIDList() // 二级目录
   }
   ```
   
5. 模板中通过el-option把List相关数据信息展示出来

   ```html
   <el-form-item label="学科：">
     <el-select v-model="addForm.subjectID">
       <el-option
                  v-for="item in subjectIDList"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
               ></el-option>
     </el-select>
   </el-form-item>
   <el-form-item label="目录：">
     <el-select v-model="addForm.catalogID">
       <el-option
                  v-for="item in catalogIDList"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
               ></el-option>
     </el-select>
   </el-form-item>
   <el-form-item label="企业：">
     <el-select v-model="addForm.enterpriseID">
     </el-select>
   </el-form-item>
   <el-form-item label="城市：">
     <el-select v-model="addForm.province" @change="getCitys(addForm.province)">
       <el-option v-for="item in provinces()" :key="item" :label="item" :value="item">
       </el-option>
     </el-select>
     <el-select v-model="addForm.city">
       <el-option 
                  v-for="item in cityList" 
                  :key="item" 
                  :label="item" 
                  :value="item"></el-option>
     </el-select>
   </el-form-item>
   <el-form-item label="方向：">
     <el-select v-model="addForm.direction">
       <el-option v-for="item in directionList" :key="item" :value="item" :label="item">
       </el-option>
     </el-select>
   </el-form-item>
   ```
   


## 企业表单域绘制

`步骤`：

1. 制作data成员enterpriseIDList

   ```js
   enterpriseIDList: [], // 企业
   ```
   

   
2. import导入获取标签数据 的list(companysList)方法(api/hmmm/companys.js)

   ```js
   import { list } from '@/api/hmmm/companys' // 企业
   ```
   

   
3. 给methods声明getEnterpriseIDList()方法，调用companysList获得标签数据，并赋予给enterpriseIDList

   ```js
   // 获得 企业 列表信息
   async getEnterpriseIDList() {
     var rst = await List()
     this.enterpriseIDList = rst.data.items
   }
   ```
   

   
4. 在created中调用getEnterpriseIDList方法

   ```js
   this.getEnterpriseIDList() // 获得企业
   ```
   

   
5. 模板中通过el-option把catalogIDList数据信息以下拉列表形式展示出来

   ```html
   <el-form-item label="企业：">
     <el-select v-model="addForm.enterpriseID">
       <el-option
                  v-for="item in enterpriseIDList"
                  :key="item.id"
                  :label="item.shortName"
                  :value="item.id"
               ></el-option>
     </el-select>
   </el-form-item>
   ```
   


`注意`：

1. 获得回来的数据信息需要调用**items**获得  this.enterpriseIDList = rst.data.items

2. 数据遍历要走 **id**和**shortName**关键字段



## 题型表单域绘制(单选按钮)

`步骤`：

1. import导入获取标签数据 的questionType常量 并设置别名questionTypeList

   ```js
   import {
     questionType as questionTypeList
   } from '@/api/hmmm/constants'
   ```
   
2. 制作data成员

   ```js
   questionTypeList, // 题型 (简易成员赋值)
   addForm:{
     questionType: '1', // 默认“单选” 题型 项目被选中(要求是字符串)
   }
   ```



3. 模板中通过  el-radio-group 和 el-radio  组件对questionTypeList数据做遍历展示

   ```html
   <el-form-item label="题型：">
     <el-radio-group v-model="addForm.questionType">
       <el-radio 
                 v-for="item in questionTypeList" 
                 :key="item.value" 
                 :label=" item.value+'' ">
         {{item.label}}
       </el-radio>
     </el-radio-group>
   </el-form-item>
   ```



`注意`：

1. el-radio-group对多个radio进行分组，并利用v-model**设置或接收**选中的项目
2. el-radio真实起作用的value数据信息要通过**label**属性定义
3. 服务器端要求题型的信息为**String**，所以设置 item.value+''



## 难度表单域绘制(单选按钮)

`步骤`：

1. import导入获取标签数据 的 difficulty 常量 并设置别名 difficultyList

   ```js
   import {
     difficulty as difficultyList
   } from '@/api/hmmm/constants'
   ```
   
2. 制作data成员

   ```js
   difficultyList, // 难度 简易成员赋值
   addForm:{
     difficulty: '1', // 默认 难度 第一个项目被选中(要求是字符串)
   }
   ```
   
3. 模板中通过el-radio组件对 difficultyList 数据做遍历展示

   ```html
   <el-form-item label="难度：">
     <el-radio-group v-model="addForm.difficulty">
       <el-radio v-for="item in difficultyList" :key="item.value" :label=" item.value+'' ">
         {{item.label}}
       </el-radio>
     </el-radio-group>
   </el-form-item>
   ```



`注意`：

1. el-radio-group对多个radio进行分组，并利用v-model**设置或接收**选中的项目
2. el-radio真实起作用的数据信息要通过**label**属性定义
3. 服务器端要求难度的信息为String，所以设置 **item.value+''**



## 普通文本域和文本框绘制

`步骤`：

1. 制作各个表单域

```html
<el-form-item label="题干：">
  <el-input type="textarea" v-model="addForm.question"></el-input>
</el-form-item>
<el-form-item label="答案：">
  <el-input type="textarea" v-model="addForm.answer"></el-input>
</el-form-item>
<el-form-item label="备注：">
  <el-input type="textarea" v-model="addForm.remarks"></el-input>
</el-form-item>
<el-form-item label="标签：">
  <el-input type="text" v-model="addForm.tags"></el-input>
</el-form-item>
<el-form-item>
  <el-button type="primary">提交</el-button>
</el-form-item>
```

2. 给data制作表单对象成员

```js
addForm:{
  question: '', // 题干
  answer: '', // 答案
  remarks: '', // 备注
  tags: '', // 标签
  videoURL: 'http://www.xxx.com' // 解析视频
}
```

`注意`：

videoURL字段是必填的项目，信息固定即可



## 试题选项(单选按钮)制作

`步骤`：

1. 声明data成员

   ```js
   // 感知被被选中的项目的值，是中间成员，需要通过watch转变为isRight
   singleSelect: '', 
   
   addForm:{
     // 选项表单数据对象部分
     options: [
       // {code: '编号ABCD', title: '当前项目文字答案', 
       //   img: '当前项目图片答案', isRight: boolean表明当前项目是否是答案},
       { code: 'A', title: '', img: '', isRight: false },
       { code: 'B', title: '', img: '', isRight: false },
       { code: 'C', title: '', img: '', isRight: false },
       { code: 'D', title: '', img: '', isRight: false }
     ]
   }
   ```
   

   
2. 绘制4组单选按钮，各个单选按钮有label属性，取值分别为 0/1/2/3

   ```html
   <el-form-item label="选项：">
     <el-radio v-model="singleSelect" :label="0">
       A: <el-input type="text" v-model="addForm.options[0]['title']"></el-input>
     </el-radio><br />
     <el-radio v-model="singleSelect" :label="1">
       B: <el-input type="text" v-model="addForm.options[1]['title']"></el-input>
     </el-radio><br />
     <el-radio v-model="singleSelect" :label="2">
       C: <el-input type="text" v-model="addForm.options[2]['title']"></el-input>
     </el-radio><br />
     <el-radio v-model="singleSelect" :label="3">
       D: <el-input type="text" v-model="addForm.options[3]['title']"></el-input>
     </el-radio>
   </el-form-item>
   ```
   
> 使得各个单选按钮的el-input输入框直接与title成员联系
   
3. 创建**watch监听器**，监听singleSelect，根据值情况设置对应项目的isRight为true

   ```js
   // watch监听器
   watch: {
     // 监听选项选中要把isRight的值做设置操作
     singleSelect(newval) {
       // 要使得全部的isRight变为false
       // newval代表的当前项目的isRight变为true
       for (var i = 0; i < 4; i++) {
         this.addForm.options[i].isRight = false
       }
       this.addForm.options[newval].isRight = true
     }
   }
   ```



## 实现试题添加

`步骤`：

1. 给添加按钮，并设置事件 @click="addQuestion()"

   ```html
   <el-button type="primary" @click="addQuestion()">提交</el-button>
   ```
   
2. import导入api接口，questions.js---》add

   ```js
   import { add } from '@/api/hmmm/questions' // 试题
   ```
   
3. 制作methods方法addQuestion，调用add(this.addForm)方法实现数据添加

   ```js
   // 收集表单数据，完成添加操作
   async addQuestion() {
     // 注意：要使得数据完成添加后，再做列表页面重定向操作
     await add(this.addForm) // 添加数据
     this.$message.success('添加数据成功')
     this.$router.push('/questions/list')// 路由重定向跳转
   },
   ```
   


`注意`：

1. addQuestion要使用async和await保证数据完成添加，再做页面跳转，显示列表
2. 数据添加，如果服务器端返回**422**错误，这表示表单域数据类型不正确，可通过浏览器firebug查看调试



## 单选、多选、简答 切换

`步骤`：

1. 声明data成员控制显示

```js
radioShow: true, // 默认显示单选项目
allShow: true, // 单选或多选默认显示一个
```

> radioShow:true   显示单选
>
> radioShow:false  显示多选
>
> allShow:true 单选或多选显示一个
>
> allShow:false 单选和多选都不显示

2. 通过监听器设置切换动作

```js
  watch: {
    // 对题型进行监听
    'addForm.questionType': function(newval) {
      // console.log(newval)
      if (Number(newval) === 1) {
        // newval=1 单选
        this.radioShow = true
        this.allShow = true
      } else if (Number(newval) === 2) {
        // newval=2 多选
        this.radioShow = false
        this.allShow = true
      } else {
        // newval=3 简答
        this.allShow = false
      }
    }
  }
```



3. 制作 复选框项目组，并和   单选框项目组 做判断显示

```html
<el-form-item label="选项：" v-if="allShow">
  <template v-if="radioShow">
    <!--单选选项组-->
    <el-radio :label="0" v-model="singleSelect">A.
      <el-input type="text" v-model="addForm.options[0].title"></el-input>
    </el-radio>
    <br>
    <el-radio :label="1" v-model="singleSelect">B.
      <el-input type="text" v-model="addForm.options[1].title"></el-input>
    </el-radio>
    <br>
    <el-radio :label="2" v-model="singleSelect">C.
      <el-input type="text" v-model="addForm.options[2].title"></el-input>
    </el-radio>
    <br>
    <el-radio :label="3" v-model="singleSelect">D.
      <el-input type="text" v-model="addForm.options[3].title"></el-input>
    </el-radio>
  </template>

  <template v-else>
    <!--多选选项组-->
    <!--复选框的v-model直接对isRight进行绑定，
而单选框不能对isRight绑定，如果绑定了它们就是4个不同的单选按钮，
造成结果是多个单选项目都可以被选中了，这与业务是相违背的-->
    <el-checkbox v-model="addForm.options[0].isRight">A.
      <el-input type="text" v-model="addForm.options[0].title"></el-input>
    </el-checkbox>
    <br>
    <el-checkbox v-model="addForm.options[1].isRight">B.
      <el-input type="text" v-model="addForm.options[1].title"></el-input>
    </el-checkbox>
    <br>
    <el-checkbox v-model="addForm.options[2].isRight">C.
      <el-input type="text" v-model="addForm.options[2].title"></el-input>
    </el-checkbox>
    <br>
    <el-checkbox v-model="addForm.options[3].isRight">D.
      <el-input type="text" v-model="addForm.options[3].title"></el-input>
    </el-checkbox>
  </template>
</el-form-item>
```




`注意`：

单选按钮组 是通过**singleSelect** 接收被选中项目，而 复选框组 是直接通过data子成员**isRight**接收



# 题库数据分页

> 在questions.vue中进行

`步骤`：

1. 编辑分页组件，及各个相关属性

   ```html
   <el-pagination
                  @size-change="handleSizeChange"
                  @current-change="handleCurrentChange"
                  :current-page="searchForm.page"
                  :page-sizes="[5, 10, 15, 20]"
                  :page-size="searchForm.pagesize"
                  layout="total, sizes, prev, pager, next, jumper"
                  :total="tot"
                  >
   </el-pagination>
   ```
   
> searchForm.page：当前页码
   >
   > searchForm.pagesize：每页显示条数
   >
   > searchForm.tot：总记录条数
   
2. 在methods方法中添加分页的两个成员，分别感知 页码、条数 变化后的处理

   ```js
   // 每页条数变化的处理
   handleSizeChange(val) {
     this.searchForm.pagesize = val
   },
   // 当前页码变化的回调处理
   handleCurrentChange(val) {
     this.searchForm.page = val
   }
   ```
   
> 由于watch对searchForm做深度监听， 条数、页码变化后不用this.getQuestionsList()获得新数据
   
3. 在data成员searchForm中声明3个成员：page、pagesize、tot

   ```js
   tot: 0, // 数据总条数
   searchForm: {
     page: 1, // 默认获取第1页数据
     pagesize: 5, // 默认每页获得4条数据
   }
   ```
   
> tot与searchForm没有关系，故定义到外边也可以
   
4. 在getQuestionsList()方法中，把获得的总记录条数赋予给tot成员

   ```js
   async getQuestionsList() {
     var rst = await list(this.searchForm)
     this.questionsList = rst.data.items
     // 获得数据总条数并赋予给searchForm.tot成员
     this.tot = rst.data.counts
   }
   ```
   
5. 样式

   ```css
   .el-pagination{
     margin-top:15px;
   }
   ```
   



# 多语言切换

`步骤`：

1. 在 src/lang/en.js 和 src/lang/zh.js 文件中配置语言信息

   ```js
   // en.js:
     question: {
       'newadd': 'NewAdd',
       'manyadd': 'ManyAdd'
     },
     
   // zh.js:
     question: {
       'newadd': '新增试题',
       'manyadd': '批量导入'
     }
   ```
   

   
2. 在具体业务组件中使用语言

   语法：

   ```
   {{ $t( 语言名称 ) }}
   ```
   
```html
   <el-button type="primary" size="mini" @click="$router.push('/questions/new')">
     {{ $t('question.newadd') }}
   </el-button>
   <el-button type="danger" size="mini">{{ $t('question.manyadd') }}</el-button>
   ```
   

`注意`：

​	elementui组件库的各个组件""多语言""默认也有配置好



## 一般项目多语言切换实现(了解)

`步骤`：

1. 安装i18n( internationalization )语言包

```
yarn add vue-i18n  // 黑马面面项目已经安装了，不用重复执行
```

2. 在main.js中进行如下配置：

```js
import Vue from 'vue'
import App from './App'

import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
// 1) 引入elementui默认提供的语言包
import enLocale from 'element-ui/lib/locale/lang/en'
import zhLocale from 'element-ui/lib/locale/lang/zh-CN'
// 2) 引入i18n的模块
import VueI18n from 'vue-i18n'
// 3) Vue对i18n进行注册
Vue.use(VueI18n) // 注册完毕在组件中就可以使用$t()语法，本质是函数调用
                 // 本质是给Vue创建methods方法 Vue.prototype.$t = xxx
Vue.use(ElementUI)

// 4) 对全部(elementui和自定义的)的语言进行收集，并存储到"messages对象"中
const messages = {
  en: {
    first: 'main', // 自定义语言包
    second: 'success',
    ...enLocale // elementui语言包 与 自定义语言包合并(英文)
  },
  zh: {
    first: '主要',
    second: '成功',
    ...zhLocale // elementui语言包 与 自定义语言包合并(中文)
  }
}
// 5) 实例化i18n对象，并初始化配置默认语言 和 全部语言集
const i18n = new VueI18n({
  locale: 'zh', // 配置默认语言
  messages, // 全部语言集合
})
// 6) ElementUI对语言包进行注册，使得ElementUI可以使用各种语言
Vue.use(ElementUI, {
  i18n: (key, value) => i18n.t(key, value)
})

new Vue({
  // 7) 挂载语言包
  i18n,
  render:h=>h(App)
}).$mount('#app')
```

3. 应用，在模板中使用语言包的各种语言，例如：

```html
<el-button type="primary">{{$t('first')}}按钮</el-button>
<el-button type="success">{{$t('second')}}按钮</el-button>
```



# 文章修改状态

需要对api接口进行调整如下articles.js：

```js
export const state = data =>
  createAPI(`/articles/${data.id}/${data.state}`, 'post', data)
```

> 设置为 ${data.state}


