<template>
  <el-container class="home-container">
    <el-header class="home-header">
      <div class="header-title">
        <img class="header-icon" src="../assets/heima.png" alt="tupian" />
        <span class="header-name">电商后台管理系统</span>
      </div>
      <el-button type="info" @click="loginOut" class="header-button">退出</el-button>
    </el-header>
    <el-container>
      <el-aside :width="isClllapse ? '64px' : '200px'">
        <div class="toggle-button" @click="toggleCollapse">|||</div>
        <el-menu background-color="#333744" text-color="#fff" unique-opened router :default-active="activePath"
          :collapse="isClllapse" :collapse-transition="false" active-text-color="#409eff">
          <el-submenu v-for="(item, index) in menuLists" :key="index" :index="index + ''">
            <template slot="title">
              <i :class="iconObj[item.id]"></i>
              <span>{{ item.authName }}</span>
            </template>
            <el-menu-item @click="saveNavState('/' + subItem.path)" v-for="(subItem, index) in item.children"
              :key="index" :index="'/' + subItem.path">
              <template slot="title">
                <i class="el-icon-menu"></i>
                <span>{{ subItem.authName }}</span>
              </template>
            </el-menu-item>
          </el-submenu>
        </el-menu>
      </el-aside>
      <el-main>
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>
<script>
export default {
  data() {
    return {
      res: {
        data: [
          {
            id: 125,
            authName: '用户管理',
            path: 'users',
            children: [
              {
                id: 110,
                authName: '用户列表',
                path: 'users',
                children: [],
                order: null
              }
            ],
            order: 1
          },
          {
            id: 103,
            authName: '权限管理',
            path: 'rights',
            children: [
              {
                id: 111,
                authName: '角色列表',
                path: 'roles',
                children: [],
                order: null
              },
              {
                id: 112,
                authName: '权限列表',
                path: 'rights',
                children: [],
                order: null
              }
            ],
            order: 2
          },
          {
            id: 101,
            authName: '商品管理',
            path: 'goods',
            children: [
              {
                id: 104,
                authName: '商品列表',
                path: 'goods',
                children: [],
                order: 1
              },
              {
                id: 115,
                authName: '分类参数',
                path: 'params',
                children: [],
                order: 2
              },
              {
                id: 121,
                authName: '商品分类',
                path: 'categories',
                children: [],
                order: 3
              }
            ],
            order: 3
          },
          {
            id: 102,
            authName: '订单管理',
            path: 'orders',
            children: [
              {
                id: 107,
                authName: '订单列表',
                path: 'orders',
                children: [],
                order: null
              }
            ],
            order: 4
          },
          {
            id: 145,
            authName: '数据统计',
            path: 'reports',
            children: [
              {
                id: 146,
                authName: '数据报表',
                path: 'reports',
                children: [],
                order: null
              }
            ],
            order: 5
          }
        ],
        meta: {
          msg: '获取菜单列表成功',
          status: 200
        }
      },
      menuLists: [],
      iconObj: {
        125: 'iconfont icon-user',
        103: 'iconfont icon-tijikongjian',
        101: 'iconfont icon-shangpin',
        145: 'iconfont icon-baobiao',
        102: 'iconfont icon-danju'
      },
      isClllapse: false,
      activePath: ''
    }
  },
  created() {
    this.getMenuList()
    this.activePath = sessionStorage.getItem('activePath')
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
    },
    saveNavState(avtive) {
      sessionStorage.setItem('activePath', avtive)
      this.activePath = avtive
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
