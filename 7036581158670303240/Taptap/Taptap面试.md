# 一面

- 换肤都做过什么处理，有没有处理过可能改变尺寸的换肤
- i18n 在团队内部都做了哪些实践
- webpack 迁移 vite 遇到了哪些问题
- CI/CD 做了哪些实践
- 鉴权有了解么，jwt 如何实现踢人，session 和 jwt 鉴权的区别
- TCP 三次握手 http1.0，1.1，2 都有哪些区别
- https，为什么 https 可以防中间人攻击
- 冒泡排序

## 换肤都做过什么处理

思路 ：

1. 在`src/asset`下建立一个 scss 文件夹, 其中包含 index.scss 文件,内容如下

```scss
// light
$color-brand1: #ffcd32;
$fill-1: #fff !default;
$color-text: #3c3c3c;
$color-text-1: #757575;
$color-text-2: #222;
// dark
$dark-fill-1: #222 !default; // 品牌色
$dark-color-text: #fff;
$dark-color-text-1: rgba(255, 255, 255, 0.3);
$dark-color-text-2: $color-brand1;

```

2. 在 App.vue 文件中的 style 标签中引入, 如下所示

```vue
<template>
  <div id="app" :data-theme="style">
    <div class="name">kobe</div>
    <div class="age">41</div>
    <div class="job">basketball player</div>
  </div>
</template>
<script>
export default {
  name: 'App',
  data() {
    return {
      style: '',
    }
  },
  created() {
    setTimeout(() => {
      this.style = 'dark'
      setTimeout(() => {
        this.style = 'light'
      }, 2000)
    }, 2000)
  },
  components: {},
  methods: {
    jump(str) {
      this.$router.push({ path: str })
    },
  },
}
</script>

<style lang="scss">
@import '@/assets/scss/index.scss';
[data-theme='dark'] {
  width: 100vw;
  height: 100vh;
  background-color: $dark-fill-1;
  .name {
    color: $dark-color-text;
  }

  .age {
    color: $dark-color-text-1;
  }

  .job {
    color: $dark-color-text-2;
  }
}

[data-theme='light'] {
  width: 100vw;
  height: 100vh;
  background-color: $color-brand1;
  .name {
    color: $color-text;
  }

  .age {
    color: $color-text-1;
  }

  .job {
    color: $color-text-2;
  }
}
</style>

```

> 可以是先换肤，但是需要多少套皮肤, 相对应就需要多少套皮肤样式
