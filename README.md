# vue3.0 尝试

## 一、3.0项目初始化
1. 升级vue-cli（版本大于4.2）
2. 创建vue项目
3. 升级vue3.0目前创建 Vue 3.0 项目需要通过插件升级的方式来实现，
	vue-cli 还没有直接支持，我们进入项目目录，并输入以下指令：
```
cd projectname
vue add vue-next
```
执行上述指令后，会自动安装 vue-cli-plugin-vue-next 插件（查看[项目代码](https://github.com/vuejs/vue-cli-plugin-vue-next)），该插件会完成以下操作：
* 安装 Vue 3.0 依赖
* 更新 Vue 3.0 webpack loader 配置，使其能够支持 .vue 文件构建
* 创建 Vue 3.0 的模板代码
* 自动将代码中的 Vue Router 和 Vuex 升级到 4.0 版本，如果未安装则不会升级
* 自动生成 Vue Router 和 Vuex 模板代码
完成上述操作后，项目正式升级到 Vue 3.0，该插件暂不支持typescript
![Snipaste_2020-06-28_10-39-16.png](https://i.loli.net/2020/06/28/m3ZBONVUcaiFuyl.png)

## 二、Vue3.x 生命周期变化

**被替换**
1. beforeCreate -> setup()
2. created -> setup()

**重命名**
1. beforeMount -> onBeforeMount
2. mounted -> onMounted
3. beforeUpdate -> onBeforeUpdate
4. updated -> onUpdated
5. beforeDestroy -> onBeforeUnmount
6. destroyed -> onUnmounted
7. errorCaptured -> onErrorCaptured

**新增的**
新增的以下2个方便调试 debug 的回调钩子：
1. onRenderTracked
2. onRenderTriggered

**特别说明**
由于 Vue3.x 是兼容 Vue2.x 的语法的，因此为了保证 Vue2.x 的语法能正常在 Vue3.x 中运行，大部分 Vue2.x 的回调函数还是得到了保留。比如：虽然 beforeCreate 、 created 被 setup() 函数替代了，也就是说在 Vue3.x 中建议使用 setup()，而不是旧的API，但是如果你要用，代码也是正常执行的。

## 三、Composition API
### 3.1 setup 主执行函数
setup是Composition API的核心，也是vue3相较于以往的版本改动最为突出的点；
* `setup()`替代了`beforeCreated`和`created`；
* 当setup以对象的形式返回时，则对象的属性将会被合并到组件模板的渲染上下文；

```js
<template>
  <div class="hello">
    <p>{{count}}</p>
    <p>{{object.foo}}</p>
  </div>
</template>

<script lang="ts">
import { ref, reactive } from "vue";

export default {
  setup() {
    const count = ref(0);
    const object = reactive({ foo: "bar" });
    
    // expose to template
    return {
      count,
      object
    };
  }
};
</script>
```

需要注意的是，在`setup()`中取消了this，利用两个参数取而代之

* props，组件参数
* context，上下文信息

```js
setup(props, context) {
    // props
    // context.attrs
    // context.slots
    // context.emit
}
```

