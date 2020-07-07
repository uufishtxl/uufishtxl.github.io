---
title: 组件详解
catalog: true
tags: 
  - vue
permalink: vue_components_in_action_2.html
folder: vue
summary: 练习2：创建一个标签页组件
---

[完整的代码](https://jsfiddle.net/edith_tang/wu456nxe/3/)

组件的功能：

所有的信息都在`index.html`提供，包括：

| 1 | 默认选中标签值 (activeKey) | 写入`index.html`的Vue实例的数据中，通过`v-model`进行双向数据传输 |
| 2 | 标签文字 | 绑定在`pane`组件标签上，传递给`pane`组件 |
| 3 | 标签 ID | 绑定在`pane`组件标签上，传递给`pane`组件 |
| 4 | 标签正文 | 直接写入组件标签`<pane>`中间，所以需要在`pane`组件中进行开槽 |
| 5 | 为`<pane>`标签开槽 | `<pane>`组件标签插入在`<tabs>`组件标签中，所以同样需要在`tabs`组件的模板中开槽 | 

## 步骤一：`index.html`的`DOM`结构

`index.html`的`DOM`结构，以及创建 Vue 实例，挂载上去。

```html
<div id="app">
  <!--  1-->
  <tabs v-model="activeValue">
    <!-- 2 & 3 & 4-->
    <pane label="标签一" name="1">标签一的内容</pane>
    <pane label="标签一" name="2">标签二的内容</pane>
    <pane label="标签一" name="3">标签三的内容</pane>
  </tabs>
</div>

<script>
  var app = new Vue({
    el: '#app',
    data: {
      activeKey: '1'
    }
  })
</script>
```

## 步骤二：为`<pane>`标签在`tabs`组件上开槽

```JS
Vue.component('tabs', {
  template: '\
  <div class="tabs"> \
    <div class="tabs-bar"> \
      <!-- 标签标题的所在 --> \
    </div> \
    <div class="tabs-content"> \
      <!-- 5 为<pane>标签开槽 -->\
      <slot></slot> \
    </div> \
  </div>',
  data: function() {
    return {
      // 将接收到的props数据保存到组件自身的数据中，进行修改
      currentValue: this.value
    }
  },
  props: {
    // 接收上层通过`v-model`传递过来的数据
    value: {
      type: [String, Number]
    }
  }
})
```
## 步骤三：为标签正文内容在`pane`组件上插槽

```JS
/* 
  pane-a. 在`pane`组件中开槽，从而让组件标签中插入的内容——标签对应的正文内容直接渲染到插槽中
  pane-b. 用一个v-show来控制组件实例是否显示
  pane-c. props接收上层组件传递过来的数据
*/
// pane-a & pane-b
Vue.component('pane', {
  // name属性会在步骤四-遍历tabs的children组件时需要用到
  name: 'pane',
  template: '\
  <div class="pane" v-show="show"> \
    <slot></slot>\
  </div>\',
  data: function() {
    return {
      show: true
    }
  },
  // pane-c
  props: {
    label: {
      type: String,
      default: ''
    },
    name: {
      type: String
    }
  }
})
```
## 步骤四：在`tabs`组件通过子链`$children`建立标签的数组

```JS
//////////////tabs//////////////
Vue.component('tabs', {
  ...,
  methods: {
    getTabs() {
      // 需要通过高阶函数来找到tabs下所有的pane组件，高阶函数中的`this`不再指向Vue实例，因此需要在它的外部定义一个局部变量，指向Vue实例
      var _this = this;
      return this.$children.filter(function(item) {
        // 通过$options可以访问Vue实例的选项的键值
        item.$options.name === 'pane';
      })
    }
  }
})
```

## 步骤五：根据`currentValue`，设定`<pane>`的`show`属性，从而控制`pane`实例显示与否

```JS
Vue.component('tabs', {
  ...,
  methods: {
    ...,
    updateStatus() {
      // 返回所有的pane组件
      var tabs = this.getTabs();
      var _this = this;
      tabs.forEach(function(tab) {
        return tab.show = tab.name === _this.currentValue;
      })
    }
  }
})
```

## 步骤六：在`tabs`组件的`navList`数据中添加标签对象，并进行渲染

### 6-1 在`tabs`组件中创建一个数组，会包含不同的标签对应的对象格式的元素，囊括了每个标签的`label`和`name`数据

```JS
Vue.component('tabs', {
  ...,
  data: function() {
    return {
      navList: []
    }
  },
  methods: {
    updateNav() {
      this.navList = [];
      var _this = this;
      this.getTabs.forEach(function(pane, index) {
        _this.navList.push({
          label: pane.label,
          // 如果有name信息，那么就用name信息，否则就直接用索引值
          name: pane.name || index
        });
        // 问题，我的理解是下面这一句和上面的没有区别
        if (!pane.name) pane.name =  index;
        // 如果之前没有通过v-model传入value，从而定义默认的currentValue，那么就默认让index为0的那个标签成为默认值
        if (index === 0) {
          if (!_this.currentValue) {
            _this.currentValue = pane.name || index;
          }
        }
      });
      // 根据currentValue设置每个pane实例属性show的布尔值
      updateStatus();
    }
  }
})
```

### 6-2 渲染标签

需要做三件事情：

1.  使用`v-for`对`navList`进行遍历，将`item.label`渲染出来

2.  用数组语法赋予`tabs` classes

3.  将点击的那一个标签的`name`值赋值给`currentValue`，并释放事件到上层，通知更改。

```JS
Vue.component('tabs', {
  tempalte: '\
  <div class="tabs> \
    <div class="tabs-bar"> \
      <div \
        :class="tabCls(item)" \
        :v-for="(item, index) in navList" \
        @click="handleChange(index)" \
      ></div>\
    </div> \
    <div class="tabs-content"> \
      <slot></slot> \
    </div> \
  </div>',
  ...
})
```

#### 6-2-1 使用数组语法绑定标签`class`属性

```JS
Vue.component('tabs', {
  ...,
  methods: {
    tabCls(item) {
      return [
        'tabs-tab',
        {
          'tabs-tab-active': item.name === this.currentValue;
        }
      ]
    }
  }
})
```

#### 6-2-2 点击事件更新`currentValue`值，并通知上层组件

```JS
Vue.component('tabs', {
  ...,
  methods: {
    handleChange(index) {
      var nav = navList[index];
      var name = nav.name
      this.currentValue = name;
      this.$emit('input', name);
      // 这个on-click是由谁捕捉的，什么用？之前练习1的on-change也类似，也不是很明白什么作用
      this.$emit('on-click', name);
    }
  }
})
```
## 步骤 7：Watch (不懂watch的时机)



### 步骤 7-1：`tabs`组件的 watch

watch 两个值：

-   上层组件通过`v-model`传递过来的数据，也就是`value`

-   自身的`currentValue`的值

```JS
Vue.component('tabs', {
  ...,
  watch: {
    value: function(val) {
      this.currentValue = val;
    },
    // 自身currentValue变化时，需要更新所有下层`pane`组件的show属性的布尔值，从而对 DOM 进行重新渲染
    currentValue: function() {
      this.updateStatus();
    }
  }
})
```

### 步骤7-2：`pane`组件的 watch

随着每次点击事件，都要伴随`label`的更新，可以直接通过父链$parent来调用父组件的方法

```JS
Vue.component('pane', {
  ...,
  methods: {
    updateNav() {
      this.$parent.updateNav();
    }
  },
  watch: {
    label() {
      this.updateNav();
    }
  },
  mounted: {
    this.updateNav();
  }
})
```

[计算属性与侦听官方说明](https://cn.vuejs.org/v2/guide/computed.html)