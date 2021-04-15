<template>
  <div></div>
</template>
<script>
export default {
  data() {
    return {
      menuLists: [],
      iconObj: {
        125: 'iconfont icon-user',
        103: 'iconfont icon-tijikongjian',
        101: 'iconfont icon-shangpin',
        145: 'iconfont icon-baobiao',
        102: 'iconfont icon-danju'
      },
      isClllapse: false
    }
  },
  created() {
    this.getMenuList()
  },
  methods: {
    loginOut() {
      sessionStorage.clear('TOKEN')
      this.$router.push('/login')
    },
    async getMenuList() {
      const res = await this.$http.get('menus')
      if (res && res.meta && res.meta.status === 200) {
        this.menuLists = res.data
      } else {
        this.$message.error(
          (res && res.meta && res.meta.msg) || '服务器异常，请稍后再试'
        )
      }
      console.log('res', res)
    },
    toggleCollapse() {
      this.isClllapse = !this.isClllapse
    }
  }
}
</script>
<style lang="less" scoped>
.el-header {
  background-color: #373d41;
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 20px;
  color: #fff;
  > div {
    display: flex;
    align-items: center;
    > span {
      margin-left: 10px;
    }
  }
}
.el-aside {
  background-color: #333744;
  .el-menu {
    border-right: 0;
  }
}
.el-main {
  background-color: #eaedf1;
}
.home-container {
  width: 100%;
  height: 100%;
}
.iconfont {
  margin-right: 10px;
}
.toggle-button {
  color: #fff;
  font-size: 10px;
  line-height: 24px;
  letter-spacing: 0.2em;
  text-align: center;
  background-color: #4a5064;
  cursor: pointer;
}
</style>
