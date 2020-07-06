<template>
    <div class="outdiv">
        <cli-title class="titleClass" ></cli-title>
        <cli-menu class="menuClass" :pageIndex="pageIndex" ></cli-menu>
        <div class="bodyClass" v-if="ifshow">
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 60px; min-height: 300px;">
                <div class="titleDiv">
                    <p class="titleMsg" >情感分析检测</p>
                </div>
                <div  style="display: table; width: 100%; padding-left: 10px; padding-top: 20px; padding-bottom:15px; padding-right: 10px;text-align: center">
                    <div style="display: table-row">
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                    </div>
                </div>
            </el-card>
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 20px; min-height: 300px;">
                <div class="titleDiv">
                    <p class="titleMsg" >老人义工交互检测</p>
                </div>
                <div  style="display: table; width: 100%; padding-left: 10px; padding-top: 20px; padding-bottom:15px; padding-right: 10px;text-align: center">
                    <div style="display: table-row">
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                    </div>
                </div>
            </el-card>
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 20px; min-height: 300px;">
                <div class="titleDiv">
                    <p class="titleMsg" >跌倒检测</p>
                </div>
                <div  style="display: table; width: 100%; padding-left: 10px; padding-top: 20px; padding-bottom:15px; padding-right: 10px;text-align: center">
                    <div style="display: table-row">
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                    </div>
                </div>
            </el-card>
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 20px; min-height: 300px;">
                <div class="titleDiv">
                    <p class="titleMsg" >陌生人检测</p>
                </div>
                <div  style="display: table; width: 100%; padding-left: 10px; padding-top: 20px; padding-bottom:15px; padding-right: 10px;text-align: center">
                    <div style="display: table-row">
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                    </div>
                </div>
            </el-card>
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 20px; min-height: 300px;">
                <div class="titleDiv">
                    <p class="titleMsg" >禁入区域检测</p>
                </div>
                <div  style="display: table; width: 100%; padding-left: 10px; padding-top: 20px; padding-bottom:15px; padding-right: 10px;text-align: center">
                    <div style="display: table-row">
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
                        <div class="tableTitle">
                        </div>
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