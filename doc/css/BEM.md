#  聊一聊BEM设计模式在Vue组件开发中的应用
回想一下在你的前端生涯中是否遇到过以下问题
1.在写css的时候经常会在命名class时绞尽脑汁
2.在团队多人开发中出现css命名冲突
3.在进行组件化开发时如何规范书写css

### 什么是BEM
BEM是Yandex团队提出的一种css的命名方式，通过这种命名方式可以很好地解决上面遇到的问题，提高css的开发效率和可读性

### 进入BEM的世界

* B: 表示块，可以抽象成一个组件
* E: 表示元素，组件下的一个元素，多个元素形成一个组件
* M:表示修饰符，可以用来表示元素的状态，比如激活状态，颜色，大小

BEM这货究竟张啥样呢，颜值高不高，请看下面的代码

```css    
    .block {}
    .block__element {}
    .block__element--modifier {}
```
看完后你的内心会不会在想,卧槽，这货居然这么丑，名字还这么长，丑拒...

### __和--连接符这是什么鬼
* __主要用来表示块(B)和元素(E)间的连接
* --用来表示块或者元素与状态的连接

比如我们要做写一个button的组件，可以这么来

```css
    
    /* 有一个叫button的组件 */
    .button {
         dispaly: inline-block;
         pading: 10px;
     } 

    /* btn组件下面有一个显示图标的元素 */
    .button__icont {
          font-size: 12px;
     }
    
    /* btn组件有好多颜色可以选择  */
    .button--primary {
        background: blue;
    }

    .button--success {
        background: green;
     }

    .button--warning {
        background: red;
     }
    
```

``` html
    <div class="button button--primary">
        <span class="button__text">蓝色按钮</span>
    </div>

   <div class="button button--success">
        <span class="button__text">绿色按钮</span>
    </div>

   <div class="button button--warning">
        <span class="button__text">红色按钮</span>
    </div>     
```

#### 在Vue中结合Stylus预编译器使用BEM规范

```

<template>
  <div class="button" :class="[type ? 'button--primary' : '']">
    <i class="button__icon"></i>
    <span class="button__text"> {{ text }} </span>
  </div>
</template>

<style lang="stylus" rel="stylesheet/stylus" scoped>
  .button
    background: #dedede
    &__icon
      font-size: 12px
    &__text
      color: #fff
    &--primary
      background: blue;
    &--success
      background: green
</style>

<script type="text/ecmascript-6">
  export default {
    props: {
      type: {
            type: String
      },
      text: {
            type: String
       }
    },
    data () {
      return {}
    },
    components: {}
  }
</script>

```




