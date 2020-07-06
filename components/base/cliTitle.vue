<template >
    <div id="out_div" style="display: table; box-shadow: 0 0 5px rgba(158,158,158,0.7); text-align: center">
      <img src="../../assets/image/s1.png" height="80%" style="position: absolute; top: 7px; left: 9px"/>
      <p style="  font-family:'黑体'; word-spacing: 10px;font-size: 25px; color: rgb(255,255,255);">智慧养老系统</p>
        <i class="el-icon-question" style="position: absolute; top: 20px; right: 70px;font-size:20px;color: white"></i>
        <i class="el-icon-message" style="position: absolute; top: 20px; right: 110px;font-size:20px;color: white"></i>
        <i class="el-icon-bell" style="position: absolute; top: 20px; right: 150px;font-size:20px;color: white"></i>
        <div style="position: absolute; top: 8px; right: 20px;">
            <img src="../../static/3.png" style="border-radius: 50%;width: 30px;height: 30px;">
        </div>
    </div>
</template>

<script>
  import API from '../../api'
  import Cookies from 'js-cookie'
  import PRO from '../../api/API_PRO.js'

    export default {
        name: "cliTitle",

      data () {
        return {
          state:'',

          /**
           * 0是普通用户
           * 1是管理员
           * 2是评委
           * **/
          roleType:Cookies.get('type'),
        }
      },

      methods: {
        querySearchAsync (queryString, cb) {
          let token = Cookies.get('token')
          let data = {
            token: token,
            keyword: queryString
          }
          API.searchProject(data).then(res => {
            this.restaurants = res.list
            clearTimeout(this.timeout)
            this.timeout = setTimeout(() => {
              //let results = queryString ? this.restaurants.filter(this.createStateFilter(queryString)) : this.restaurants
              let results = queryString ?this.createStateFilter(this.restaurants): this.restaurants
              console.log(results)
              cb(results)
            }, 3000 * Math.random())
          }).catch(msg => {
            let results = queryString ?this.createStateFilter(this.restaurants): this.restaurants
            cb(results)
          })
        },
        createStateFilter (restaurants) {
          let results = []
          restaurants.forEach(item=>{
            results.push({'content':((item.projectName) + '-' + (item.principalInfo.name  )+ '-' + (item.principalInfo.phone)), 'projectId':item.projectId})
          })
          return results
        },
        //查看详情
        gocliNoticeDetail(item) {
          if (Cookies.get('type') === '0') {
            //普通用户跳转到管理页面
            //this.$router.push({path: '/processManagement/_paperId/userProcess?projectId='+item.projectId})
            this.$router.push({path:'/refreshPage?url='+'/processManagement/_paperId/userProcess?projectId='+item.projectId})
          }else if (Cookies.get('type') === '1') {
            //管理员
            //this.$router.push({path: '/project/cliProDetailPage?projectId='+item.projectId})
            this.$router.push({path:'/refreshPage?url='+'/project/cliProDetailPage?projectId='+item.projectId})
          }
        }
        }
    }
</script>

<style scoped>
  #out_div{
    width: 100%;
    height: 60px;
    top:0;
    background-color: #00CCFF;
    z-index: 9999;
      line-height: 60px;
  }
</style>
