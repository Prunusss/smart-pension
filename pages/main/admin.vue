<template>
    <div class="outDiv">
        <cli-title class="titleClass"></cli-title>
        <cli-menu class="menuClass" :pageIndex="pageIndex"></cli-menu>

        <div class="bodyClass">
<!--            <notify_list_table :showType="showType" style="width: 100%; margin-top: 20px;margin-bottom: 30px"> </notify_list_table>-->

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

            <div>

<!--                <div class="body2">-->
<!--                    <position :positionName="position2.name1"-->
<!--                              :have-back="position2.haveBack"-->
<!--                              :rightName="position2.name2"-->
<!--                              @positionBack="click2"-->
<!--                              style="font-size:22px"-->
<!--                    ></position>-->
<!--                    <list :roleType="roleType" style="width: 100%; margin-top: 20px;margin-bottom: 30px"></list>-->
<!--                </div>-->

            </div>
        </div>


    </div>
</template>

<script>
    import Cookies from 'js-cookie'
    import List from "../../components/message/list";
    import CliTitle from "../../components/base/cliTitle";
    import CliMenu from "../../components/base/cliMenu";
    import Position from "../../components/base/position";
    import DataEdit from "../../components/message/message_edit";
    import Message_detail from "../../components/message/message_detail";
    import Notify_list_table from "../../components/notify/notify_list_table";
    export default {
        name: "admin",
        components: {Notify_list_table, Message_detail, DataEdit, Position, CliMenu, CliTitle,List},

        data(){
            return{
                pageIndex: "1",
                position1: {
                    name1: '通知',
                    name2: '更多',
                    haveBack: true,

                },
                position2: {
                    name1: '问卷收集',
                    name2: '更多',
                    haveBack: true,

                },


                viewType: false,
                showType:2,
                roleType: Cookies.get('type')
            };
        },

        methods:{

            click1(){
                this.$router.push({path: `/notify`})
            },
            click2(){
                this.$router.push({path: `/message`})
            }
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
