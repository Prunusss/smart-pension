<template>
  <div id="scrollHid" style="align-items: center; background-color:rgb(244, 249, 255);padding-right: 0;height:1200px;max-height: 1500px">

      <el-menu
        :default-active="activeIndex"
        class="el-menu-vertical-demo"
        @open="handleOpen"
        @close="handleClose"
        background-color="#545c64"
        text-color="#fff"
        active-text-color="#fff"
      >
        <el-menu-item class="menuItem" index="1"  @click=toCLiHomePage  style="padding: 0"  >
          <div v-bind:class="{ 'menuclick': (pageIndex === '1') }"  style="font-family: '微软雅黑 Light'; width:100%;font-size: 14px">首页</div>
        </el-menu-item>
        <el-menu-item class="menuItem" index="2"  @click=toCLiAuditorPage  style="padding: 0; " >
          <div v-bind:class="{ 'menuclick': (pageIndex === '2') }"  style="font-family: '微软雅黑 Light'; width:100%;font-size: 14px"  >系统设置</div>
        </el-menu-item>
        <el-menu-item class="menuItem" index="3"  @click="toOldInfoPage" style="padding: 0; ">
          <div v-bind:class="{ 'menuclick': (pageIndex === '3') }"  style="font-family: '微软雅黑 Light'; width:100%;font-size: 14px"  >老人信息管理</div>
        </el-menu-item>
        <el-menu-item class="menuItem" index="4"  @click="toWorkerInfoPage" style="padding: 0; ">
          <div v-bind:class="{ 'menuclick': (pageIndex === '4') }"  style="font-family: '微软雅黑 Light'; width:100%;font-size: 14px"  >工作人员管理</div>
        </el-menu-item>
        <el-menu-item class="menuItem" index="5"  @click="toVolunteerInfoPage" style="padding: 0; ">
          <div v-bind:class="{ 'menuclick': (pageIndex === '5') }"  style="font-family: '微软雅黑 Light'; width:100%;font-size: 14px"  >义工信息管理</div>
        </el-menu-item>
        <el-menu-item class="menuItem" index="6"  @click=toCliNoticePage style="padding: 0; ">
          <div v-bind:class="{ 'menuclick': (pageIndex === '6') }"  style="font-family: '微软雅黑 Light'; width:100%;font-size: 14px"  >数据管理</div>
        </el-menu-item>
        <el-menu-item class="menuItem" index="7"  @click=toCameraPage style="padding: 0; ">
          <div v-bind:class="{ 'menuclick': (pageIndex === '7') }"  style="font-family: '微软雅黑 Light'; width:100%;font-size: 14px"  >摄像头管理</div>
        </el-menu-item>

        <el-menu-item class="menuItem" index="8" @click="toProcessManagementPage" style="padding: 0; ">
          <div v-bind:class="{ 'menuclick': (pageIndex === '8') }"  style="font-family: '微软雅黑 Light'; width:100%;font-size: 14px"  >用户管理</div>
        </el-menu-item>


        <el-menu-item class="menuItem"   index="9" style="padding: 0; " @click="toSettingPage">
          <div v-bind:class="{ 'menuclick': (pageIndex === '9') }"  style="font-family: '微软雅黑 Light'; width:100%;font-size: 14px"  >个人设置</div>
        </el-menu-item>

        <el-menu-item class="menuItem"   index="10" style="padding: 0; " @click="logout">
          <div v-bind:class="{ 'menuclick': (pageIndex === '10') }"  style="font-family: '微软雅黑 Light'; width:100%;font-size: 14px">退出</div>
        </el-menu-item>

      </el-menu>

    <el-dialog
      title="温馨提示"
      :visible.sync="centerDialogVisible"
      width="30%"
      center>
      <span>页面正在开发，敬请期待</span>
      <span slot="footer" class="dialog-footer">
    <el-button type="primary" @click="centerDialogVisible = false">确 定</el-button>
  </span>
    </el-dialog>
  </div>
</template>

<script>
  import Cookies from 'js-cookie'
  import Pro from '../../api/API_PRO'
  import API from "../../api"
    export default {
        name: "cliMenu",
      props:{
        pageIndex: {
          type: String
        }
      },
      data () {
        return {
          activeIndex: "1",
          name:'',
          account_name:'',
          isadmin: false,
          centerDialogVisible:false,
          isShowdefMan:false,
          isShowJudge:false,
          id:'',

          /**
           *  '0': 管理员
           *  '1'：普通用户
           * */
          type: Cookies.get('type'),
        }
      },
      mounted:function () {
          this.getOriginalInfo()
        this.activeIndex = this.pageIndex
      },
      methods: {
        getOriginalInfo(){
          let data ={
            token: this.token,
          }
          API.Getinfo(data).then(res => {
            if(res.code){
              alert(res.message);
              return;
            }

            this.account_name = res.user_info.name;
            console.log(res);
          }).catch(msg => {
            if(res.code){
              alert(res.message);
              return;
            }
            alert(msg)
          })
        },
        handleOpen(key, keyPath) {
          console.log(key, keyPath);
        },
        handleClose(key, keyPath) {
          console.log(key, keyPath);
        },
        toonline(){
          if(this.id==2) {
            this.$router.push({path: `/review/start/online/judge/judgepage`})
          }
          else if(this.id==0) {
            this.$router.push({path: `/review/start/online/user/useron`})
          }
          else if(this.id==1) {
            this.$router.push({path: `/testPage`})
          }
          this.activeIndex = "111"
        },
        tooffline(){
          if(this.id==1) {
            this.$router.push({path: `/review/start/offline/admin/adminpage`})
          }
          else if(this.id==0) {
            this.$router.push({path: `/review/start/offline/user/useroff`})
          }
          this.activeIndex = "112"
        },
        toCLiHomePage(){
          if(this.type === '0') {
            this.$router.push({path: `/main/admin`})
          } else if (this.type === '1'){
            this.$router.push({path: `/main/user`})
          }
          this.activeIndex = "1"
        },
        toCLiAuditorPage(){
          this.$router.push({path: `/notify`})
          this.activeIndex = "3"
        },
        toCliProjectList(){
          this.$router.push({path: `/project/cliProjectListPage`})
          this.activeIndex = "3"
        },
        toCliNoticePage(){
          this.$router.push({path: `/message`})
          this.activeIndex = "6"
        },

        toPaperPage() {
           this.$router.push({ path: '/paper/personal_paper'});
           this.activeIndex = "4";
        },
        toPaperPageHome() {
          this.$router.push({ path: '/paper'});
          this.activeIndex = "4";
        },

        toProcessManagementPage(){
          if (this.isadmin === true) {
            this.$router.push({path: `/person`})
          } else {
            this.$router.push({path: '/person'})
          }
          this.activeIndex = "8"
        },
        toSpacePage(){
          this.$router.push({path: `/space`})
          this.activeIndex = "9"
        },
        toDownloadPage(){
          this.$router.push({path: `/download`})
          this.activeIndex = "21"
        },
        toJixiaoPage() {
          this.$router.push({path: `/jixiao`})
          this.activeIndex = "10"
        },
        toDatalistPage(){
          this.$router.push({path: `/datalist`})
          this.activeIndex = "11"
        },
        toSettingPage(){
          this.$router.push({path: '/person/user'})
        },
        toPercenterPage(){
          this.$router.push({path: '/personalCenter/cliPercenterPage'})
          this.activeIndex = "7"
        },
        toOldInfoPage(){
          this.$router.push({path: '/old'})
          this.activeIndex = "3"
        },
        toWorkerInfoPage(){
          this.$router.push({path: '/worker'})
          this.activeIndex = "4"
        },
        toVolunteerInfoPage(){
          this.$router.push({path: '/volunteer'})
          this.activeIndex = "5"
        },
        toCameraPage(){
          this.$router.push({path: '/personalCenter/cliPercenterPage'})
          this.activeIndex = "7"
        },
        logout(){
          // this.$router.push({path: `/`})
          const redirect_uri = Pro.qianduanURL;
          const url = `https://cas.bjtu.edu.cn/auth/logout?next=${redirect_uri}`
          window.location.replace(url);
        },
        showdialog(){
          this.centerDialogVisible = true
        },
        showDefMan(){
          if(this.isShowdefMan)
            this.isShowdefMan = false;
          else
            this.isShowdefMan = true;
        },
        showJudge(){
          if(this.isShowJudge)
            this.isShowJudge = false;
          else
            this.isShowJudge = true;
        }
      }
    }
</script>

<style scoped>
  .el-menu-vertical-demo{
    text-align:center;
    height: 2850px;
    width: 100%;
  }

  .menuclick {
    background:linear-gradient(to right,#55DDFF 5%, #3B8DA2 5%);
    /*background:linear-gradient(to right,rgb(51,167,242) 5%, rgb(48,166,243) 5%)*/

  }

  .pic{
    width: 80px;
    height: 80px;

  }

  .menuItem{
    height: 40px;
    line-height: 40px;
    margin-top: 5px;
  }

  .pic img{
    width: 100%;
    border-radius: 80%;
  }
  #scrollHid::-webkit-scrollbar{
    display: none;
  }
  #scrollHid>ul{
    height: 1500px;
  }

</style>
<style>
  .el-submenu .el-menu-item{
    min-width: 0;

    padding:0;
    padding-left: 0!important;
  }
  .el-menu-item-group__title{
    padding: 0;
    padding-left: 0!important;
  }
  .el-submenu__title{
    padding: 0;
    padding-left: 0!important;

  }
  /*.el-menu-item div{*/
  /*  text-align: left;*/
  /*  padding-left: 20px;*/
  /*}*/


</style>
