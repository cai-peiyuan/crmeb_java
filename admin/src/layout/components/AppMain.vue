<template>
  <section class="app-main">
    <transition name="fade-transform" mode="out-in">
      <keep-alive :include="cachedViews">
        <router-view :key="key" />
      </keep-alive>
    </transition>

    <!-- 底部信息 连接和版权 -->
    <div class="footers" v-if="showFooter">
      <el-link v-for="item in links" :key="item.key" :href="item.href" target="_blank" class="mr15 mb20">{{item.title}}</el-link>
      <div class="title mb15" v-text="copyright"></div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AppMain',
  data () {
    return {
      showFooter: false,
      links: [
        {
          title: '官网',
          key: '1',
          href: 'https://www.crmeb.com',
          blankTarget: true
        },
        {
          title: '社区',
          key: '2',
          href: 'https://q.crmeb.net/?categoryId=122&sequence=0',
          blankTarget: true
        },
        {
          title: '文档',
          key: '3',
          href: 'https://help.crmeb.net/crmeb_java/1748037',
          blankTarget: true
        }
      ],
      copyright: 'Copyright © 2024'
    }
  },
  computed: {
    cachedViews() {
      return this.$store.state.tagsView.cachedViews
    },
    key() {
      return this.$route.path
    }
  }
}
</script>

<style lang="scss" scoped>
  .footers{
    text-align: center;
    font-size: 14px;
    color: #808695;
    .title{
      font-size: 14px;
      color: #808695;
    }
  }
.app-main {
  /* 50= navbar  50  */
  min-height: calc(100vh - 50px);
  width: 100%;
  position: relative;
  overflow: hidden;
}

.fixed-header+.app-main {
  padding-top: 50px;
}

.hasTagsView {
  .app-main {
    background: #f5f5f5;
    /* 84 = navbar + tags-view = 50 + 34 */
    min-height: calc(100vh - 84px);
    overflow-y: scroll;
  }

  .fixed-header+.app-main {
    padding-top: 80px;
  }
}
.el-popup-parent--hidden {
  .fixed-header {
    padding-right: 15px;
  }
}
</style>

