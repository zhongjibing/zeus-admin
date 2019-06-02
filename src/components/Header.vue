<template>
  <header class="app-header navbar" id="header">
    <button class="navbar-toggler mobile-sidebar-toggler d-lg-none" type="button" @click="mobileSidebarToggle">&#9776;</button>
    <b-link class="navbar-brand" to="#"></b-link>
    <button class="navbar-toggler sidebar-toggler d-md-down-none" type="button" @click="sidebarMinimize">&#9776;</button>
    <b-nav is-nav-bar class="d-md-down-none">
      <b-nav-item class="px-3">Dashboard</b-nav-item>
      <b-nav-item class="px-3">Users</b-nav-item>
      <b-nav-item class="px-3">Settings</b-nav-item>
    </b-nav>
    <b-nav is-nav-bar class="ml-auto">
      <b-nav-item class="d-md-down-none">
        <i class="icon-bell"></i><span class="badge badge-pill badge-danger">5</span>
      </b-nav-item>
      <b-nav-item class="d-md-down-none">
        <i class="icon-list"></i>
      </b-nav-item>
      <b-nav-item class="d-md-down-none">
        <i class="icon-location-pin"></i>
      </b-nav-item>
      <b-nav-item-dropdown right>
        <template slot="button-content">
          <img src="static/img/avatars/6.jpg" class="img-avatar" alt="admin@bootstrapmaster.com">
          <span id="loginUser" class="d-md-down-none">{{userName}}</span>
        </template>
        <!-- <b-dropdown-header tag="div" class="text-center"><strong>Account</strong></b-dropdown-header> -->
        <!-- <b-dropdown-item><i class="fa fa-bell-o"></i> Updates<span class="badge badge-info">42</span></b-dropdown-item>
        <b-dropdown-item><i class="fa fa-envelope-o"></i> Messages<span class="badge badge-success">42</span></b-dropdown-item>
        <b-dropdown-item><i class="fa fa-tasks"></i> Tasks<span class="badge badge-danger">42</span></b-dropdown-item>
        <b-dropdown-item><i class="fa fa-comments"></i> Comments<span class="badge badge-warning">42</span></b-dropdown-item>
        <b-dropdown-header tag="div" class="text-center"><strong>Settings</strong></b-dropdown-header>
        <b-dropdown-item><i class="fa fa-user"></i> Profile</b-dropdown-item>
        <b-dropdown-item><i class="fa fa-wrench"></i> Settings</b-dropdown-item>
        <b-dropdown-item><i class="fa fa-usd"></i> Payments<span class="badge badge-default">42</span></b-dropdown-item>
        <b-dropdown-item><i class="fa fa-file"></i> Projects<span class="badge badge-primary">42</span></b-dropdown-item>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item><i class="fa fa-shield"></i> Lock Account</b-dropdown-item> -->
        <b-dropdown-item v-on:click="userProfile"><i class="fa fa-user"></i> Profile</b-dropdown-item>
        <b-dropdown-item v-on:click="logout"><i class="fa fa-lock"></i> Logout</b-dropdown-item>
      </b-nav-item-dropdown>
    </b-nav>
    <button class="navbar-toggler aside-menu-toggler d-md-down-none" type="button" @click="asideToggle">&#9776;</button>
  </header>
</template>
<script>
  import axios from 'axios'
  import request from '../../config/request'

  export default {
    name: 'header',
    mounted: function() {
      this.load();
    },
    data: function() {
      return {
        userName: ''
      };
    },
    methods: {
      load () {
        let self = this;
        let requestUrl = request.request.REQUEST + '/profile/current';
        axios({
          method: 'get',
          url: requestUrl,
          headers: {'Content-Type': 'application/x-www-form-urlencoded;charset=utf-8'},
          params: {}
        })
          .then(function (res) {
            if (res.data.code === 0) {
              self.userName = res.data.resp && res.data.resp.userName;
            } else {
              console.error(res.data.msg);
            }
          })
          .catch(function (err) {
            console.log(err)
          });
      },
      sidebarToggle (e) {
        e.preventDefault()
        document.body.classList.toggle('sidebar-hidden')
      },
      sidebarMinimize (e) {
        e.preventDefault()
        document.body.classList.toggle('sidebar-minimized')
      },
      mobileSidebarToggle (e) {
        e.preventDefault()
        document.body.classList.toggle('sidebar-mobile-show')
      },
      asideToggle (e) {
        e.preventDefault()
        document.body.classList.toggle('aside-menu-hidden')
      },
      logout: function () {
        localStorage.clear();
        document.cookie = 'user=;expires=' + new Date().toGMTString()
        this.$router.push({ path: '/login' })
      },
      userProfile:function () {
        this.$router.push({ path: '/systemManager/UserProfile' });
      }
    }
  }
</script>
