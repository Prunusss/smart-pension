<template>
    <el-card shadow="hover" :body-style="{ padding: '0px' }">
        <div  style="display: table; width: 100%; padding-left: 10px; padding-top: 20px; padding-bottom: 20px; padding-right: 10px">
            <div style="display: table-row">
                <div class="tableTitle" style="width: 5%; text-align: center;padding-left: 10px">
                    #
                </div>
                <div class="tableTitle" style="width: 30%; text-align: center">
                    名称
                </div>
                <div class="tableTitle" style="width: 20%; text-align: center" v-if="type==='0'">
                    完成度
                </div>
                <div class="tableTitle" style="text-align: center">
                    问卷填写周期
                </div>
                <div class="tableTitle" style="text-align: center" >
                    发布时间
                </div>
                <div class="tableTitle" style="text-align: center" v-if="type==='1'">
                    状态
                </div>
                <div class="tableTitle" style="width: 50px" >
                </div>
                <div v-if="type === '0'" class="tableTitle" style="width: 50px" >
                </div>

            </div>
            <div :class="{'tablerow':true, 'grayLine': (index % 2 === 0)}" style="display: table-row;" v-if="item.name.split('/')[1] === accountinfo&&surveyList.length > 0" v-for="(item,index) in surveyList" :key="item.id">
                <div class="tableCell" style="width: 5%; text-align: center; " >
                    ·
                </div>
                <div class="tableCell" style="width: 30%; text-align: center">
                    {{item.name.split('/')[0]}}
                </div>
                <div class="tableCell" style="width: 20%; text-align: center" v-if="type==='0'">
                    <el-progress :text-inside="true" :stroke-width="26" :percentage="item.infopercentage" :color="percentageColor"></el-progress>
                </div>
                <div class="tableCell" style="text-align: center">
                    {{getDate(item.start_timestamp)}} - {{getDate(item.stop_timestamp)}}
                </div>
                <div class="tableCell" style="text-align: center">
                    {{item.create_time}}
                </div>
                <div class="tableCell" style="text-align: center" v-if="item.is_submit===0&&roleType!=='0'">
                    未填写
                </div>
                <div class="tableCell" style="text-align: center" v-if="item.is_submit===1&&roleType!=='0'">
                    已填写
                </div>
                <div class="tableCell"  style="width: 50px; text-align: center">
                    <el-button class ="detail" size="mini" @click="readNotify(item)" >详情</el-button>
                </div>
                <div v-if="type === '0'" class="tableCell"  style="width: 50px; text-align: center">
                    <el-button class ="detail" size="mini" @click="deleteZhengji(item)" >删除</el-button>
                </div>

            </div>
        </div>

        <div v-if="!inMain" class="paginaClass">
            <el-pagination
                    @current-change=currentChange
                    :current-page.sync=currentPage
                    :page-size="pageSize"
                    layout="prev, pager, next, jumper"
                    :total=total
                    style="">
            </el-pagination>
            <div style="padding-right: 15px" v-if="type === '0'">
                <el-button type="primary" size="mini" @click="toNewMessage">新增问卷</el-button>
            </div>
        </div>

    </el-card>
</template>

<script>
    import Cookies from 'js-cookie'
    import API from '../../api'

    export default {
        props: {
            roleType: {String}
        },
        data(){
            return{
                accountinfo:0,
                inMain:false,
                hidden:true,
                total:0,
                pageSize:30,
                currentPage:1,
                token: Cookies.get('token'),
                surveyList:{},
                type: Cookies.get('type'),
                percentageColor:'#409eff',
            }
        },

        mounted:function(){
            let ourinfo = Cookies.get('info')
            let sndinfo = ourinfo.split(',')[1]
            this.accountinfo = sndinfo.split(':')[1]
            this.isInMain();
            this.getSurveyList();
        },

        methods:{
            isInMain () {
                this.inMain = this.$route.path === '/main/admin';
            },
            currentChange(val){
                this.currentPage = val;
                this.getSurveyList();
            },
            /**
             * 计算发布时间
             * */
            getDate(timestamp) {
                var now = new Date(timestamp),
                y = now.getFullYear(),
                m = now.getMonth() + 1,
                d = now.getDate();
                return y + "-" + (m < 10 ? "0" + m : m) + "-" + (d < 10 ? "0" + d : d) + " "
            },
            /**
             * 获取问卷列表
             * */
            getSurveyList(){
                // 判断是否在首页
                this.inMain = this.$route.path === '/main/admin';
                if (this.inMain) {
                    let data ={
                        token: this.token,
                        orderby: {},
                        page: 1,
                        size: 5,
                    };
                    API.surveylist(data).then(res => {
                        if(res.code){
                            alert(res.message);
                            return;
                        }

                        this.surveyList = res.list;
                        this.total = res.count;
                        this.calMesPercentage();
                        return res;

                    }).catch(msg => {
                        alert('操作失败')
                    })
                } else {
                    let data ={
                        token: this.token,
                        orderby: {},
                        page: this.currentPage,
                        size: this.pageSize,
                    }
                    if(this.type==0)
                    {
                        API.surveylist(data).then(res => {
                        if(res.code){
                            alert(res.message);
                            return;
                        }

                        this.surveyList = res.list;
                        this.total = res.count;
                        this.calMesPercentage();
                        return res;
                    }).catch(msg => {
                        alert('操作失败')
                    })
                    }else{
                        API.userSurveylist(data).then(res => {
                            if(res.code){
                                alert(res.message);
                                return;
                            }

                            this.surveyList = res.list;
                            this.total = res.count;
                            this.calMesPercentage();
                            return res;

                        }).catch(msg => {
                            alert('操作失败')
                        })

                    }

                }
            },
            /**
             * 计算完成度
             * */
            calMesPercentage () {
                this.surveyList.forEach(item => {
                    let per = item.submit_num / (item.submit_num + item.unsubmit_num) * 100;
                    if (isNaN(per)) per = 0;
                    var standper;
                    if (Number.isInteger(per)) {
                        standper = per;
                    } else {
                        standper = per.toFixed(1);
                    }
                    item.infopercentage = standper;
                })
            },
            /**
             * 阅读
             * */
            readNotify(item){
                if (this.type === '0') {
                    this.$router.push({path: `/message/${item.id}/admin_detail`});
                } else {
                    this.$router.push({path: `/message/${item.id}/user_detail`});
                }
            },

            deleteZhengji(item) {

                this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                }).then(() => {
                    let data = {
                        token: this.token,
                        survey_id: item.id,
                    }

                    API.deleteZhengji(data).then(res => {
                        if(res.code){
                            alert(res.message);
                            return;
                        }
                        this.getSurveyList();
                        alert('删除成功');

                    }).catch(msg => {
                        alert('操作失败')
                    })
                }).catch(() => {
                    this.$message({
                        type: 'info',
                        message: '已取消删除'
                    });
                });

            },

            toNewMessage(){
                this.$router.push({path: `/message/add`})
            }
        }
    }
</script>

<style scoped>
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
        font-size: 10px;
        color: #11A0FF;
    }

    .tableTitle{
        display: table-cell;
        font-size: 15px;
        padding: 5px;
        font-family: 黑体;
        font-weight: bold;
        color: rgb(128, 128, 128);

    }
    .tableCell{
        display: table-cell;
        font-size: 15px;
        padding: 5px;
        /*color:rgb(128, 128, 128);*/
    }
    .grayLine{
        background-color: #e4efff;
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
    .detail{
        display: table-cell;
        color: #fff;
        background: rgb(80, 137, 185);
    }
    .state{
        display: table-cell;
        font-size: 13px;
        padding: 5px;
        color:rgb(80, 137, 185);
        font-weight: bolder;
    }
    .paginaClass{
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-left: 5%;
        padding-bottom: 15px;
        padding-top: 10px;
    }

    .el-progress-bar__innerText{
        color: #000;
        font-weight: bold;
    }

</style>
