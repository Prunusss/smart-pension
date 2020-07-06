<template>
    <div class="outdiv">
        <cli-title class="titleClass" ></cli-title>
        <cli-menu class="menuClass" :pageIndex="pageIndex" ></cli-menu>
        <div class="bodyDiv" v-if="ifshow">
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 60px; min-height: 300px;">
                <div class="titleDiv">
                    <p class="titleMsg" >通知</p>
                    <p class="showAll" @click="to_notify_page">查看全部</p>
                </div>
                <div  style="display: table; width: 100%; padding-left: 10px; padding-top: 20px; padding-bottom:15px; padding-right: 10px;text-align: center">
                    <div style="display: table-row">
                        <div class="tableTitle" style="width: 40%; text-align: center;padding-left: 10px">
                            标题
                        </div>
                        <div class="tableTitle" style="width: 25%; text-align: center">
                            时间
                        </div>
                        <div class="tableTitle" style="width: 20%; text-align: center">
                            发布人
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
                        <div class="tableCell fist" style="text-align: left;padding-left: 50px; " >
                            <!--                            {{item.title}}-->
                            测试
                        </div>
                        <div class="tableCell" style="text-align: center">
                            <!--                            {{item.create_time}}-->
                            2020-07-04 10:34
                        </div>
                        <div class="tableCell" style="text-align: center">
                            <!--                            {{item.publisherInfo.name}}-->
                            李涛
                        </div>
                        <div class="tableCell"  style="width: 50px">
                            <el-button size="mini" @click="readNotify(item)" >详情</el-button>
                        </div>
                        <div class="tableCell" style="width: 50px">
                            <el-button size="mini" @click="deleteNotifyList(item)">删除</el-button>
                        </div>
                        <div class="tableCell" style="width: 70px">
                            <el-button size="mini" @click="toUnRead(item)">3人未读 | {{5}}人已读</el-button>
                        </div>
                    </div>
                    <div :class="{'tablerow':true, 'grayLine': (1 === 0)}" style="display: table-row;" >
                        <div class="tableCell fist" style="text-align: left;padding-left: 50px; " >
                            <!--                            {{item.title}}-->
                            写个假的
                        </div>
                        <div class="tableCell" style="text-align: center">
                            <!--                            {{item.create_time}}-->
                            2020-07-04 10:34
                        </div>
                        <div class="tableCell" style="text-align: center">
                            <!--                            {{item.publisherInfo.name}}-->
                            李涛
                        </div>
                        <div class="tableCell"  style="width: 50px">
                            <el-button size="mini" @click="readNotify(item)" >详情</el-button>
                        </div>
                        <div class="tableCell" style="width: 50px">
                            <el-button size="mini" @click="deleteNotifyList(item)">删除</el-button>
                        </div>
                        <div class="tableCell" style="width: 70px">
                            <el-button size="mini" @click="toUnRead(item)">3人未读 | {{5}}人已读</el-button>
                        </div>
                    </div>
                    <div :class="{'tablerow':true, 'grayLine': (1 === 1)}" style="display: table-row;" >
                        <div class="tableCell fist" style="text-align: left;padding-left: 50px; " >
                            <!--                            {{item.title}}-->
                            啦啦啦
                        </div>
                        <div class="tableCell" style="text-align: center">
                            <!--                            {{item.create_time}}-->
                            2020-07-04 10:34
                        </div>
                        <div class="tableCell" style="text-align: center">
                            <!--                            {{item.publisherInfo.name}}-->
                            李涛
                        </div>
                        <div class="tableCell"  style="width: 50px">
                            <el-button size="mini" @click="readNotify(item)" >详情</el-button>
                        </div>
                        <div class="tableCell" style="width: 50px">
                            <el-button size="mini" @click="deleteNotifyList(item)">删除</el-button>
                        </div>
                        <div class="tableCell" style="width: 70px">
                            <el-button size="mini" @click="toUnRead(item)">3人未读 | {{5}}人已读</el-button>
                        </div>
                    </div>
                </div>
                <div  style="display: flex; align-items: center; justify-content: space-between;margin-left: 5%; padding-bottom: 15px; padding-top: 10px">
                    <div></div>

                    <div style="padding-right: 15px" >
                        <el-button type="primary" size="mini" @click="toNewNotify">新增公告</el-button>
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
                pageIndex: "3",
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
</style>





