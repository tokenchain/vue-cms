<template>
  <el-menu
    class="navbar"
    mode="horizontal" 
    text-color="#fff"
    active-text-color="#fff">
    <router-link to="/home">
      <el-menu-item index="1">后台管理系统</el-menu-item>
    </router-link>
    <el-dropdown class="avatar-container" trigger="click">
      <div class="avatar-wrapper">
        <img class="user-avatar" :src="avatar">
        <div class="username-wrapper">
          <span class="user-name">{{name}}</span>
          <i class="el-icon-caret-bottom"></i>
        </div>
      </div>
      <el-dropdown-menu class="user-dropdown" slot="dropdown">
        <router-link class='inlineBlock' to="/user/profile">
          <el-dropdown-item>
            个人中心
          </el-dropdown-item>
        </router-link>
        <router-link class='inlineBlock' to="/user/profile">
          <el-dropdown-item>
            修改头像
          </el-dropdown-item>
        </router-link>
        <!-- <a target='_blank' href="https://github.com/PanJiaChen/vue-element-admin/">
          <el-dropdown-item>
            项目地址
          </el-dropdown-item>
        </a> -->
        <el-dropdown-item @click.native="logout">
          <span style="display:block;">退出登录</span>
        </el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
  </el-menu>
</template>
<script>
  import { mapGetters, mapActions } from 'vuex'
  export default {
    name: '',
    computed: {
      ...mapGetters([
        'name',
        'avatar'
      ])
    },
    methods: {
      ...mapActions({
        userLogout: 'logout'
      }),
      logout() {
        this.userLogout().then(() => {
          location.reload()// 为了重新实例化vue-router对象 避免bug
        }).catch(err => {
          console.log(err)
        })
      }
    }
  }
</script>
<style scoped lang="scss">
  .navbar {
    position: fixed;
    width: 100%;
    z-index: 10;
    background: {
      image: -webkit-gradient(linear, left top, right top, from(#1278f6), to(#00b4aa));
      image: -webkit-linear-gradient(45deg, #1278f6, #00b4aa 50%, #1278f6);
      image: -moz-linear-gradient(45deg, #1278f6, #00b4aa 50%, #1278f6);
      image: linear-gradient(45deg,#1278f6,#00b4aa 50%, #1278f6);
    }
  }
  .navbar /deep/ .el-menu-item {
    &:hover {
      background-color: transparent;
    }
    &:focus {
      background-color: transparent;
    }
  }
  .avatar-container {
    position: absolute;
    top: 15px;
    right: 40px;
    color: #fff;
    .avatar-wrapper {
      cursor: pointer;
      .user-avatar {
        width: 30px;
        height: 30px;
        border-radius: 50%;
        vertical-align: middle;
      }
      .username-wrapper {
        display: inline-block;
        height: 30px;
        line-height: 30px;
      }
    }
  }
</style>