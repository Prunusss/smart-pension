<template>
    <div class="outdiv">
        <cli-title class="titleClass" ></cli-title>
        <cli-menu class="menuClass" :pageIndex="pageIndex" ></cli-menu>
        <div class="bodyClass">
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 60px; min-height: 300px;">
                <div class="titleDiv">
                    <p class="titleMsg" >情感分析检测</p>
                </div>
                <div style="display: table; width: 100%; padding: 20px 15px 15px;text-align: center">
                    <el-row>
                        <el-col :span="8" v-for="(o, index) in 6" :key="o" >
                            <el-card :body-style="{ padding: '0px' }" style="margin-bottom: 20px;margin-right: 20px">
                                <img src="../../static/kk.jpg" class="image" @click="showEmo">
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
        <el-dialog title="" :visible.sync="show_emotion" :modal="true" width="40%" >
            <div style="font-family:'黑体';font-weight: bold; word-spacing: 10px;font-size: 20px;margin-top: -40px">情感分析</div>
            <div style="margin: 10px -20px; border-style: solid none solid none">
            <div v-loading="isLoading" style="margin:15px 20px 0 30px;width: 450px;height:320px;" id="echartss"></div>
            </div>
        </el-dialog>

    </div>
</template>

<script>
    import cliTitle from '~/components/base/cliTitle.vue'
    import cliMenu from '~/components/base/cliMenu.vue'
    import Cookies from 'js-cookie'
    import echarts from 'echarts'
    import API from '../../api'


    export default {
        name: "notify_list",
        //通知列表
        components: {cliTitle, cliMenu},
        data(){
            return{
                pageIndex: "6",
                show_emotion: false,
                isLoading: true,
                vueEmoData:[],
            }
        },
        mounted:function () {
            let emotion = {'愤怒': 91.283, '厌恶': 5.008, '恐惧': 3.523, '开心': 0.009, '正常': 0.008, '伤心': 0.032, '惊讶': 0.135};
            let emKeys = ['愤怒','厌恶','恐惧','开心','正常','伤心','惊讶'];
            // let vueEmoData = [];

            for(var i=0;i<7;i++) { //便历每一条数据
                this.vueEmoData.push({
                    name:emKeys[i],
                    value:emotion[emKeys[i]]
                });
            }
            console.log(this.vueEmoData);
        },
        methods:{
            clickBack(){
                this.$router.push({path: `/main/admin`})
            },
            showEmo(){
                /*
                *': {
                * 'anger': 96.283,
                * 'disgust': 0.008,
                * 'fear': 3.523,
                * 'happiness': 0.009,
                * 'neutral': 0.008,
                * 'sadness': 0.032,
                * 'surprise': 0.135
                * }
                */

                this.show_emotion = true;
                if (document.getElementById('echartss')){
                    // 基于准备好的dom，初始化echarts实例
                    let myChart = echarts.init(document.getElementById('echartss'))
                    // 绘制图表，this.echarts1_option是数据
                    myChart.setOption({
                        // color: ['#DDF1FF', 'rgb(239,242,239)','rgb(106,184,216)', 'rgb(254,240,240)','rgb(253,246,236)'],/*饼状图的颜色*/
                        color: ['rgb(3,149,255)', 'rgb(73,136,248)','rgb(138,215,246)', 'rgb(199,237,248)','rgb(162,238,243)'],
                        //标题
                        title: {
                            text: '情感分析',
                            // subtext:'各种情绪占比',
                            x:'center',
                            textStyle: {
                        }
                        },
                        //弹窗，响应鼠标指向，显示具体细节
                        tooltip : {
                            trigger: 'item',//以具体项目触发弹窗
                            formatter: "{a} <br/>{b} : {c} ({d}%)"
                        },
                        //图例，选择要显示的项目
                        legend:{
                            orient:'vertical',
                            left:'left',
                            textStyle:{
                            // color:'#c8c8d0',
                            color: 'black',
                            },
                            data:['愤怒','厌恶','恐惧','开心','正常','伤心','惊讶']  //注意要和数据的name相对应
                        },
                        //工具箱
                        toolbox:{
                            show:true,//显示工具箱
                            feature:{
                                dataView:{show:true}, //以文字形式显示数据
                                restore:{show:true},   //还原
                                saveAsImage:{show:true},  //保存图片
                            }
                        },
                        //数据
                        series : [
                            {
                                name:'情绪',
                                type:'pie',
                                radius : '60%',
                                center: ['50%', '60%'],
                                // data:[
                                //     {value:10, name:'开心'},
                                //     {value:3, name:'伤心'},
                                //     {value:5, name:'惊讶'},
                                //     {value:7, name:'生气'},
                                //     {value:15, name:'害怕'}
                                // ],
                                data:this.vueEmoData,
                                itemStyle: {
                                    emphasis: {
                                        shadowBlur: 10,
                                        shadowOffsetX: 0,
                                        shadowColor: 'rgba(0, 0, 0, 0.5)'
                                    },
                                    normal: {
                                        borderWidth: 2,/*隔开的白色边界*/
                                        borderColor: '#fff',/*border*/
                                        // labelLine :{show:true}
                                    },
                                },
                                label: { //饼图图形的文本标签
                                    normal: {  //下同，normal指在普通情况下样式，而非高亮时样式
                                        textStyle: {
                                            color: 'rgb(3,149,255)'
                                        }
                                    }
                                },
                                labelLine: {  //引导线样式
                                    normal: {
                                        lineStyle: {
                                            color: 'rgb(3,149,255)'
                                        },
                                    }
                                },
                            }
                        ],
                    });
                    this.isLoading = false;
                }
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