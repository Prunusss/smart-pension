<template>
    <div class="outdiv">
        <cli-title class="titleClass" ></cli-title>
        <cli-menu class="menuClass" :pageIndex="pageIndex" ></cli-menu>
        <div class="bodyClass" v-if="ifshow">
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 60px; min-height: 300px;">
                <div class="titleDiv">
                    <p class="titleMsg" >情感分析检测</p>
                </div>
                <div style="display: table; width: 100%; padding: 20px 15px 15px;text-align: center">
                    <el-row>
                        <el-col :span="8" v-for="(o, index) in 6" :key="o" >
                            <el-card :body-style="{ padding: '0px' }" style="margin-bottom: 20px;margin-right: 20px">
                                <img src="../../static/kk.jpg" class="image">
                                <div style="padding: 14px;">
                                    <span style="font-weight: bold">事件：情感检测</span>
                                    <div class="bottom clearfix">
                                        <span style="float: left">老人姓名：姓名{{index}}</span>
                                        <span style="color: #999;float: right">{{'2020/7/6 00:00:00'}}</span>
                                    </div>
                                </div>
                            </el-card>
                        </el-col>
                    </el-row>
                </div>
            </el-card>
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 20px; min-height: 300px;">
                <div class="titleDiv" style="background-color: rgb(239,242,239)">
                    <p class="titleMsg" >老人义工交互检测</p>
                </div>
                <div style="display: table; width: 100%; padding: 20px 15px 15px;text-align: center">
                    <el-row>
                        <el-col :span="8" v-for="(o, index) in 6" :key="o" >
                            <el-card :body-style="{ padding: '0px' }" style="margin-bottom: 20px;margin-right: 20px">
                                <img src="../../static/kylin.jpg" class="image">
                                <div style="padding: 14px;">
                                    <span style="font-weight: bold">事件：老人义工交互检测</span>
                                    <div class="bottom clearfix">
                                        <span style="float: left">老人姓名：姓名{{index}}</span>
                                        <span style="color: #999;float: right">{{'2020/7/6 00:00:00'}}</span>
                                    </div>
                                </div>
                            </el-card>
                        </el-col>
                    </el-row>
                </div>
            </el-card>
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 20px; min-height: 300px;">
                <div class="titleDiv" style="background-color: rgb(254,240,240)">
                    <p class="titleMsg" >跌倒检测</p>
                </div>
                <div style="display: table; width: 100%; padding: 20px 15px 15px;text-align: center">
                    <el-row>
                        <el-col :span="8" v-for="(o, index) in 6" :key="o" >
                            <el-card :body-style="{ padding: '0px' }" style="margin-bottom: 20px;margin-right: 20px">
                                <img src="../../static/kk.jpg" class="image">
                                <div style="padding: 14px;">
                                    <span style="font-weight: bold">事件：跌倒检测</span>
                                    <div class="bottom clearfix">
                                        <span style="float: left">老人姓名：姓名{{index}}</span>
                                        <span style="color: #999;float: right">{{'2020/7/6 00:00:00'}}</span>
                                    </div>
                                </div>
                            </el-card>
                        </el-col>
                    </el-row>
                </div>
            </el-card>
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 20px; min-height: 300px;">
                <div class="titleDiv" style="background-color: rgb(253,246,236)">
                    <p class="titleMsg" >陌生人检测</p>
                </div>
                <div style="display: table; width: 100%; padding: 20px 15px 15px;text-align: center">
                    <el-row>
                        <el-col :span="8" v-for="(o, index) in 6" :key="o" >
                            <el-card :body-style="{ padding: '0px' }" style="margin-bottom: 20px;margin-right: 20px">
                                <img src="../../static/kylin.jpg" class="image">
                                <div style="padding: 14px;">
                                    <span style="font-weight: bold">事件：陌生人检测</span>
                                    <div class="bottom clearfix">
                                        <span style="float: left">陌生人进入！{{index}}</span>
                                        <span style="color: #999;float: right">{{'2020/7/6 00:00:00'}}</span>
                                    </div>
                                </div>
                            </el-card>
                        </el-col>
                    </el-row>
                </div>
            </el-card>
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 20px; min-height: 300px;">
                <div class="titleDiv" style="background-color: rgb(254,240,240)">
                    <p class="titleMsg" >禁入区域检测</p>
                </div>
                <div style="display: table; width: 100%; padding: 20px 15px 15px;text-align: center">
                    <el-row>
                        <el-col :span="8" v-for="(o, index) in 6" :key="o" >
                            <el-card :body-style="{ padding: '0px' }" style="margin-bottom: 20px;margin-right: 20px">
                                <img src="../../static/kk.jpg" class="image">
                                <div style="padding: 14px;">
                                    <span style="font-weight: bold">事件：禁入区域检测</span>
                                    <div class="bottom clearfix">
                                        <span style="float: left">闯入禁入区域！{{index}}</span>
                                        <span style="color: #999;float: right">{{'2020/7/6 00:00:00'}}</span>
                                    </div>
                                </div>
                            </el-card>
                        </el-col>
                    </el-row>
                </div>
            </el-card>
        </div>

    </div>
</template>

<script>
    import cliTitle from '~/components/base/cliTitle.vue'
    import cliMenu from '~/components/base/cliMenu.vue'
    import notifyTable from '~/components/notify/notify_list_table.vue'
    import notifyStuTable from '~/components/notify/notify_list_table_stu.vue'
    import Cookies from 'js-cookie'
    import API from '../../api'
    import Position from "../../components/base/position";


    export default {
        name: "notify_list",
        //通知列表
        components: {Position, cliTitle, cliMenu, notifyTable, notifyStuTable},
        data(){
            return{
                pageIndex: "6",
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
            // if (Number.parseInt(Cookies.get("type")) === 1){
            //     this.showType = 2
            //
            // } else {
            //     this.showType = 1
            // }
            this.ifshow = true
        },
        methods:{
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
    }
    .titleMsg{
        font-family: 黑体;
        font-size: 20px;
    }
    .tableTitle{
        display: table-cell;
        font-size: 15px;
        padding: 5px;
        font-family: 黑体;
        font-weight: bold;

    }
    .bodyClass{
        min-width: 850px;
        margin-left: 150px;
        padding: 20px;
    }
    .bottom {
        margin-top: 13px;
        line-height: 12px;
    }

    .button {
        padding: 0;
        float: right;
    }

    .image {
        width: 100%;
        height: 200px;
        display: block;
    }

    .clearfix:before,
    .clearfix:after {
        display: table;
        content: "";
    }

    .clearfix:after {
        clear: both
    }
</style>