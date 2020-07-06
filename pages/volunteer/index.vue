<template>
    <div class="outdiv">
        <cli-title class="titleClass" ></cli-title>
        <cli-menu class="menuClass" :pageIndex="pageIndex" ></cli-menu>
        <div class="bodyClass" v-if="ifshow">
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 60px; min-height: 300px;">
                <div class="titleDiv">
                    <p class="titleMsg" >义工信息管理</p>
                    <!--                    <p class="showAll" @click="to_notify_page">查看全部</p>-->
                </div>
                <div  style="display: table; width: 100%; padding-left: 10px; padding-top: 20px; padding-bottom:15px; padding-right: 10px;text-align: center">
                    <div style="display: table-row">
                        <div class="tableTitle" style="text-align: center;padding-left:20px;width: 40px">

                        </div>
                        <div class="tableTitle" style="text-align: center">
                            姓名
                        </div>
                        <div class="tableTitle" style="text-align: center">
                            性别
                        </div>
                        <div class="tableTitle" style="text-align: center">
                            手机
                        </div>
                        <div class="tableTitle" style="text-align: center">
                            身份证号
                        </div>
                        <div class="tableTitle" style="text-align: center">
                            生日
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                    </div>
                    <div :class="{'tablerow':true, 'grayLine': (1 === 1)}" style="display: table-row;" >
                        <div class="tableCell" style="text-align: center;vertical-align:middle;padding-left:20px;width: 40px">
                            <!--                            {{item.title}}-->
                            <img src="../../static/3.png" style="border-radius: 50%;width: 40px;height: 40px;">
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.create_time}}-->
                            2020-07-04 10:34
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.publisherInfo.name}}-->
                            李涛
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.create_time}}-->
                            2020-07-04 10:34
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.create_time}}-->
                            2020-07-04 10:34
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.publisherInfo.name}}-->
                            李涛
                        </div>
                        <div class="tableCell"  style="width: 50px;vertical-align:middle;">
                            <el-button size="mini" @click="readNotify(item)" >详情</el-button>
                        </div>
                        <div class="tableCell" style="width: 50px;vertical-align:middle;">
                            <el-button size="mini" @click="update(item)">编辑</el-button>
                        </div>
                        <div class="tableCell" style="width: 70px;vertical-align:middle;">
                            <el-button size="mini" @click="deleteNotifyList(item)">删除</el-button>
                        </div>
                    </div>
                    <div :class="{'tablerow':true, 'grayLine': (1 === 0)}" style="display: table-row;" >
                        <div class="tableCell" style="text-align: center;vertical-align:middle;padding-left:20px;width: 40px">
                            <!--                            {{item.title}}-->
                            <img src="../../static/3.png" style="border-radius: 50%;width: 40px;height: 40px;">
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.create_time}}-->
                            2020-07-04 10:34
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.publisherInfo.name}}-->
                            李涛
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.create_time}}-->
                            2020-07-04 10:34
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.create_time}}-->
                            2020-07-04 10:34
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.publisherInfo.name}}-->
                            李涛
                        </div>
                        <div class="tableCell"  style="width: 50px;vertical-align:middle;">
                            <el-button size="mini" @click="readNotify(item)" >详情</el-button>
                        </div>
                        <div class="tableCell" style="width: 50px;vertical-align:middle;">
                            <el-button size="mini" @click="update(item)">编辑</el-button>
                        </div>
                        <div class="tableCell" style="width: 70px;vertical-align:middle;">
                            <el-button size="mini" @click="deleteNotifyList(item)">删除</el-button>
                        </div>
                    </div>
                    <div :class="{'tablerow':true, 'grayLine': (1 === 1)}" style="display: table-row;" >
                        <div class="tableCell" style="text-align: center;vertical-align:middle;padding-left:20px;width: 40px">
                            <!--                            {{item.title}}-->
                            <img src="../../static/3.png" style="border-radius: 50%;width: 40px;height: 40px;">
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.create_time}}-->
                            2020-07-04 10:34
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.publisherInfo.name}}-->
                            李涛
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.create_time}}-->
                            2020-07-04 10:34
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.create_time}}-->
                            2020-07-04 10:34
                        </div>
                        <div class="tableCell" style="text-align: center;vertical-align:middle;">
                            <!--                            {{item.publisherInfo.name}}-->
                            李涛
                        </div>
                        <div class="tableCell"  style="width: 50px;vertical-align:middle;">
                            <el-button size="mini" @click="readNotify(item)" >详情</el-button>
                        </div>
                        <div class="tableCell" style="width: 50px;vertical-align:middle;">
                            <el-button size="mini" @click="update(item)">编辑</el-button>
                        </div>
                        <div class="tableCell" style="width: 70px;vertical-align:middle;">
                            <el-button size="mini" @click="deleteNotifyList(item)">删除</el-button>
                        </div>
                    </div>
                </div>
                <div  style="display: flex; align-items: center; justify-content: space-between;margin-left: 5%; padding-bottom: 15px; padding-top: 10px">
                    <div></div>

                    <div style="padding-right: 15px" >
                        <el-button type="primary" size="mini" @click="toNewNotify">新增人员</el-button>
                    </div>
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
                pageIndex: "5",
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
    .showAll{
        font-size: 12px;
        color: #11A0FF;
    }
    .tableTitle{
        display: table-cell;
        font-size: 15px;
        padding: 5px;
        font-family: 黑体;
        font-weight: bold;

    }
    .tableCell{
        display: table-cell;
        font-size: 15px;
        padding: 5px;
    }
    .fist{
        display: flex;
        position: relative;
        top: -5px;
    }
    .fist::before{
        display: block;
        content: "";
        height: 10px;
        width: 10px;
        border-radius: 5px;

        background-color: #5b8bff;
        position: relative;
        left: -25px;
        top: 5px;
    }
    .showAll:hover{
        cursor: pointer;
    }
    .bodyClass{
        min-width: 850px;
        margin-left: 150px;
        padding: 20px;
    }
    .grayLine{
        background-color: #e4efff;
    }
</style>





