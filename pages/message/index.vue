<template>
    <div class="outdiv">
        <cli-title class="titleClass" ></cli-title>
        <cli-menu class="menuClass" :pageIndex="pageIndex" ></cli-menu>
        <div class="bodyClass">
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 60px; min-height: 300px;">
                <div class="titleDiv">
                    <p class="titleMsg" >数据统计</p>
                </div>

                <div style="">
                    <div style="margin:20px 20px 20px 40px">
                        排序：
                        <el-radio-group v-model="reverse">
                            <el-radio :label="true">倒序</el-radio>
                            <el-radio :label="false">正序</el-radio>
                        </el-radio-group>
                    </div>
                    <el-timeline :reverse="reverse" style="width: 30%;display: inline-block">
                        <el-timeline-item
                                v-for="(activity, index) in activities"
                                v-if="index < 3"
                                :key="index"
                                :timestamp="activity.date"
                                placement="top">
                            <el-card>
                                <h4>{{activity.desc}}</h4>
                                <p>{{activity.location}}</p>
                            </el-card>
                        </el-timeline-item>
                    </el-timeline>
                    <div id="myChart" style="display:inline-block;margin-left:55px;margin-right:15px; width: 60%; height:350px"></div>
                </div>
            </el-card>
            <el-card shadow="hover" :body-style="{ padding: '0px' }" style="margin-top: 20px; min-height: 300px;">
                <div class="titleDiv">
                    <p class="titleMsg" >情感分析检测</p>
                </div>
                <div style="display: table; width: 100%; padding: 20px 15px 15px;text-align: center">
                    <el-row>
                        <el-col :span="8" v-for="(item, index) in emotionImgList" :key="index" >
                            <el-card :body-style="{ padding: '0px' }" style="margin-bottom: 20px;margin-right: 20px" v-show="index < 3">
                                <img :src="'data:image/jpg;base64,' + item.photo_base64.slice(2,-2)" class="image" @click="showEmo(item)">
                                <div style="padding: 14px;">
                                    <span style="font-weight: bold">事件：情感检测</span>
                                    <div class="bottom clearfix">
                                        <span style="float: left">老人姓名：xiejunxi {{index}}</span>
                                        <span style="color: #999;float: right">{{item.date}}</span>
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
                        <el-col :span="8" v-for="(item, index) in interactImgList" :key="index" >
                            <el-card :body-style="{ padding: '0px' }" style="margin-bottom: 20px;margin-right: 20px" v-show="index < 3">
                                <img :src="'data:image/jpg;base64,' + item.photo_base64.slice(2,-2)" class="image">
                                <div style="padding: 14px;">
                                    <span style="font-weight: bold">事件：老人义工交互检测</span>
                                    <div class="bottom clearfix">
                                        <span style="float: left">老人姓名：姓名{{index}}</span>
                                        <span style="color: #999;float: right">{{item.date}}</span>
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
                        <el-col :span="8" v-for="(item, index) in fallImgList" :key="index" >
                            <el-card :body-style="{ padding: '0px' }" style="margin-bottom: 20px;margin-right: 20px" v-show="index < 3">
                                <img :src="'data:image/jpg;base64,' + item.photo_base64.slice(2,-2)" class="image">
                                <div style="padding: 14px;">
                                    <span style="font-weight: bold">事件：跌倒检测</span>
                                    <div class="bottom clearfix">
                                        <span style="float: left">老人姓名：姓名{{index}}</span>
                                        <span style="color: #999;float: right">{{item.date}}</span>
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
                        <el-col :span="8" v-for="(item, index) in strangerImgList" :key="index" >
                            <el-card :body-style="{ padding: '0px' }" style="margin-bottom: 20px;margin-right: 20px" v-show="index < 3">
                                <img :src="'data:image/jpg;base64,' + item.photo_base64.slice(2,-2)" class="image">
                                <div style="padding: 14px;">
                                    <span style="font-weight: bold">事件：陌生人检测</span>
                                    <div class="bottom clearfix">
                                        <span style="float: left">陌生人进入！{{index}}</span>
                                        <span style="color: #999;float: right">{{item.date}}</span>
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
                        <el-col :span="8" v-for="(item, index) in forbiddenImgList" :key="index" >
                            <el-card :body-style="{ padding: '0px' }" style="margin-bottom: 20px;margin-right: 20px" v-show="index < 3">
                                <img :src="'data:image/jpg;base64,' + item.photo_base64.slice(2,-2)" class="image">
                                <div style="padding: 14px;">
                                    <span style="font-weight: bold">事件：禁入区域检测</span>
                                    <div class="bottom clearfix">
                                        <span style="float: left">闯入禁入区域！{{index}}</span>
                                        <span style="color: #999;float: right">{{item.date}}</span>
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
    import echarts from 'echarts'
    import axios from "axios";


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
                reverse: true,
                // activities:[],

                activities: [{
                    date: '支持使用图标',
                    desc: '2018-04-12 20:46',
                    location: 'large',
                }, {
                    date: '支持使用图标',
                    desc: '2018-04-12 20:46',
                    location: 'large',
                },{
                    date: '支持使用图标',
                    desc: '2018-04-12 20:46',
                    location: 'large',
                },{
                    date: '支持使用图标',
                    desc: '2018-04-12 20:46',
                    location: 'large',
                }],

                imageData: '',
                emotionImgList:[],
                interactImgList:[],
                strangerImgList:[],
                fallImgList:[],
                forbiddenImgList:[],
                num_emotion:0,
                num_interact:0,
                num_stranger:0,
                num_fall:0,
                num_forbidden:0,

            }
        },
        mounted:function () {
            this.drawLine();
            let emotion = {'愤怒': 91.283, '厌恶': 5.008, '恐惧': 3.523, '开心': 0.009, '正常': 0.008, '伤心': 0.032, '惊讶': 0.135};
            let emKeys = ['愤怒','厌恶','恐惧','开心','正常','伤心','惊讶'];
            // setInterval(this.useFunc,1000);

            for(let i=0; i<7; i++) { //便历每一条数据
                this.vueEmoData.push({
                    name:emKeys[i],
                    value:emotion[emKeys[i]]
                });
            }
            console.log(this.vueEmoData);
        },
        methods:{
            useFunc(){
                this.loadActivities();
                for (let i = 0; i < 5; i++){
                    this.loadEventByType(i);
                }
                this.num_forbidden = this.num_forbidden + 2;
                this.num_interact = this.num_interact + 1;
                this.num_fall = this.num_fall + 3;
                this.drawLine();
            },
            drawLine(){
                // 基于准备好的dom，初始化echarts实例
                let myChart = echarts.init(document.getElementById('myChart'))
                // 绘制图表
                myChart.setOption({
                    color: ['#fff'],
                    backgroundColor: 'rgb(244, 249, 255)', // 背景色
                    //rgb(244, 249, 255)
                    tooltip: {},
                    xAxis: {
                        name: '事件', //x轴坐标
                        data: ["情感变化","义工交互" ,"陌生人进入" ,"老人跌倒","禁入区域闯入"],
                        axisLine: { //坐标线
                            lineStyle: {
                                type: 'dashed',
                                color: '#48558C', // 轴线的颜色
                                width: '1' // 坐标线的宽度
                            },
                        },
                        axisTick: { // 刻度
                            show: false // 不显示刻度线
                        },
                        nameTextStyle: { // 标题样式
                            // color: ['#fff']
                        },
                        axisLabel: {
                            interval: 0,
                            textStyle: {
                                // color: '#fff', // 坐标值得具体的颜色
                                fontSize: 14
                            }
                        }
                    },
                    yAxis : [
                        {
                            name: '事件数量',
                            type : 'value',
                            min: 0,
                            max: 50,
                            interval: 10,
                            axisLine: { // 线
                                show: false
                            },
                            axisTick: { // 刻度
                                show: false
                            },
                            splitLine: { // 网格为虚线
                                show: true,
                                lineStyle: {
                                    type: 'dashed',
                                    color: '#48558C'
                                }
                            },
                            nameTextStyle: {
                                color: ['#48558C']
                            },
                            axisLabel: {
                                textStyle: {
                                    color: '#48558C', // 坐标值得具体的颜色
                                    fontSize: 14
                                }
                            }
                        }
                    ],
                    grid: { // 设置图标边距
                        left: '5%',
                        right: '15%',
                        bottom: '5%',
                        containLabel: true
                    },
                    legend: {
                        selectedMode: false, // 取消图例上的点击事件
                        icon: 'circle', // 图例为圆形
                        right: 15,
                        top: 10,
                        orient: 'vertical', // 纵列分布
                        itemWidth: 10, // 图例图标的宽
                        itemHeight: 10, // 图例图标的高
                        textStyle: {
                            fontSize: 12,
                            color: '#5E76D7' // 值的具体的颜色
                        }
                    },
                    series: [{
                        name: '次数',
                        type: 'bar',
                        barWidth: '50', // 设置宽度
                        data: [this.num_emotion, this.num_interact, this.num_stranger, this.num_fall, this.num_forbidden],
                        itemStyle: {
                            normal: {
                                color: '#5E76D7', // 设置柱子颜色
                                label: {
                                    show: true, // 柱子上显示值
                                    position: 'inside', // 值在柱子上方显示
                                    textStyle: {
                                        color: '#fff' // 值得颜色
                                    }
                                }
                            }
                        }
                    }]
                });
            },
            loadActivities(){
                axios.get('http://192.168.121.130:5050/api/eventlist').then(resp => {
                    if (resp.data.code === 'ERROR') {
                        alert('出现系统错误！')
                        return

                    }else{
                        this.activities  = resp.data
                    }
                })
            },
            loadEventByType(eventType){
                axios.get('http://192.168.121.130:5050/api/eventlist/'+eventType).then(resp => {
                    if (resp.data.code === 'ERROR') {
                        alert('出现系统错误！')
                        return

                    }else{
                        if (eventType === 0){
                            this.emotionImgList = resp.data;
                            this.num_emotion = this.emotionImgList.length;
                        } else if (eventType === 1){
                            this.interaImgList = resp.data;
                            this.num_interact = this.interaImgList.length;
                        } else if (eventType === 2){
                            this.strangerImgList = resp.data;
                            this.num_stranger = this.strangerImgList.length;
                        } else if (eventType === 3){
                            this.fallImgList = resp.data;
                            this.num_fall = this.fallImgList.length;
                        } else if(eventType === 4){
                            this.forbiddenImgList = resp.data;
                            this.num_forbidden = this.forbiddenImgList.length;
                        } else{
                            console.log('something wrong, the type we get does not match anyone...')
                        }
                    }
                })
            },
            clickBack(){
                this.$router.push({path: `/main/admin`})
            },
            showEmo(item){
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
                                // data:this.vueEmoData,
                                data:item.desc.split('/')[1],
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
