<template>
    <div class="outdiv">
        <cli-title class="titleClass" ></cli-title>
        <cli-menu class="menuClass" :pageIndex="pageIndex" ></cli-menu>
        <div class="bodyClass" v-if="ifshow">
            <p style="font-size:26px;margin-top: 60px;text-align: center;font-family: 黑体;">{{gettime}}</p>
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="display:inline-block;width:49%;margin-top: 20px; min-height: 400px;">
                <div class="titleDiv">
                    <p class="titleMsg" >实时监控-摄像头1</p>
                </div>
                <div  style="display: table; width: 100%; padding: 20px 10px 15px;text-align: center">
                    <img src="../../static/3.png" style="width: 440px;height: 330px;">
                </div>
            </el-card>
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="display:inline-block;width:49%;margin-left:20px;margin-top: 10px; min-height: 400px;">
                <div class="titleDiv">
                    <p class="titleMsg" >实时监控-摄像头2</p>
                </div>
                <div  style="display: table; width: 100%; padding-left: 10px; padding-top: 20px; padding-bottom:15px; padding-right: 10px;text-align: center">
                    <img src="../../static/3.png" style="width: 440px;height: 330px;">
                </div>
            </el-card>
        </div>

    </div>
</template>

<script>
    import cliTitle from '~/components/base/cliTitle.vue'
    import cliMenu from '~/components/base/cliMenu.vue'
    import Cookies from 'js-cookie'
    import API from '../../api'


    export default {
        name: "notify_list",
        //通知列表
        components: {cliTitle, cliMenu},
        data(){
            return{
                pageIndex: "7",
                gettime: '2020/7/6 00:00:00',
                token: Cookies.get('token'),
                type: Cookies.get('type'),
                ifshow:false,
                /**
                 *
                 *  2   校级通知列表
                 *  1   普通通知列表
                 */
                showType:2,
                position: {
                    name: '通知公告栏',
                    haveBack: false,

                },
            }
        },
        mounted:function () {
            this.currentTime();
            console.log(this.gettime);
            this.ifshow = true
        },
        methods:{
            getTime(){
                var _this = this;
                let yy = new Date().getFullYear();
                let mm = new Date().getMonth()+1;
                let dd = new Date().getDate();
                let hh = new Date().getHours();
                let mf = new Date().getMinutes()<10 ? '0'+new Date().getMinutes() : new Date().getMinutes();
                let ss = new Date().getSeconds()<10 ? '0'+new Date().getSeconds() : new Date().getSeconds();
                _this.gettime = yy+'/'+mm+'/'+dd+' '+hh+':'+mf+':'+ss;
            },
            currentTime(){
                setInterval(this.getTime,500)
            },
            clickBack(){
                this.$router.push({path: `/main/admin`})
            },
        }


    }
</script>

<style scoped>
    @import "../../assets/css/page/normalLayout.css";
    .titleDiv{
        background-color: #DDF1FF;
        padding: 10px 20px;

        display: flex;
        justify-content: space-between;
        align-items: center;
        text-align: center;
    }
    .titleMsg{
        font-family: 黑体;
        font-size: 20px;
        display: inline-block;
        text-align: center;
    }
    .bodyClass{
        min-width: 850px;
        margin-left: 150px;
        padding: 20px;
    }
</style>




