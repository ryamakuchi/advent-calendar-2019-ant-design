<template>
  <div>
    <a-menu v-model="current" mode="horizontal">
      <a-menu-item key="brand">
        <div class="brand-content">
          <logo />

          <a
            href="https://qiita.com/advent-calendar/2019/nuxt-js"
            target="_blank"
            rel="noopener noreferrer"
          >
            Nuxt.js Advent Calendar 2019 for Qiita
          </a>
        </div>
      </a-menu-item>

      <a-menu-item key="docs" class="float-right">
        <a
          href="https://element.eleme.io/"
          target="_blank"
          rel="noopener noreferrer"
        >
          Made with Ant Design Vue
        </a>
      </a-menu-item>
    </a-menu>

    <nuxt />
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  data() {
    return {
      current: ['brand']
    }
  }
}
</script>

<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.ant-menu {
  padding: 0 5%;
}
.ant-menu .brand-content {
  display: flex;
  padding: 10px 0;
}
.ant-menu .float-right {
  float: right;
  padding: 10px;
}
</style>
