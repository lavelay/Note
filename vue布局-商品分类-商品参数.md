# vue电商后台管理项目

## 布局template



①要有唯一的根元素

②自定义组件面包屑<my-bread/>

③element-ui组件库中    

 1.使用<el-card/>布置内容区域

2.<el-row/>布局整行内容<el-col/>布局整列内容

3.<el-table/>渲染表格时将后台获取的数据写入data属性 <el-table-column/>表格中整列属性label（名称）prop（绑定关键字=》表单验证）

4.<el-button/>按钮属性type（类型）icon（图标）

5.<el-pagination/>分页在element-ui官网复制粘贴

6.<el-tag/>用于动态编辑标签，如关闭功能

7.<el-dialog/>弹出层，都会使有属性:visible.sync=标志位控制开关

8.<el-from>表单，一般都会有属性rules（验证规则）model（绑定表单数据）ref（获取dom元素）<el-form-item/>表单单元

9.<el-cascader/>级联选择器在element-ui官网复制粘贴

10.<el-tabs/>标签页@tab-click被选中时触发<el-tab-pane/>标签单元

## 商品管理-商品分类

①初始化数据：在生命周期created中初始化参数数据

②参数分为一个参数，二级参数，三级参数，发送请求获取所有参数渲染列表

③添加分类功能，点击添加按钮打开dialog，打开后可以填写分类名称，提交时使用this.$refs.addForm.validate（）验证表单，通过后发送请求添加分类，更新数据。

④删除分类功能，分类参数渲染列表后，每行分类后面有删除按钮，使用删除固定格式，传递id参数发送请求进行删除。更新数据

this.$confirm("亲，是否删除该参数？", "提示", {

​        confirmButtonText: "确定",

​        cancelButtonText: "取消",

​        type: "warning"

​      })

​        .then(）.catch（）

⑤编辑分类功能，分类参数渲染列表后，每行参数后面有编辑按钮，打开编辑dialog，填写分类名字，传递id参数和分类名称发送请求，更新数据，清空表单，关闭对话框

## 商品管理-商品参数	

①初始化数据：在生命周期created中初始化级联选择器数据

②参数分为动态参数和静态参数，只有在级联选择器中选择三级分类时才能够获取该商品的参数，发送请求渲染列表

③添加参数功能，动态的静态的参添加  使用的对话框是同一个（标题不一样）提交：需要  三级分类ID   参数名称   参数类型，所有的业务在一个对话框实现一个添加逻辑去实现。

④删除参数功能：根据后端提供的接口  不需要类型   把动态和静态参数的删除一起实现，绑定事件：动态参数列表  静态参数列表  同时绑定了处理函数

⑤动态参数展开项：使用<el-tab v-for="item in scope.row.数据"/>遍历数据，基于<template slot-scope="scope">模板数据













