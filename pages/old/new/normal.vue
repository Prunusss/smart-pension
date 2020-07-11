<template>
    <div class="outDiv">
        <cli-title class="titleClass"></cli-title>
        <cli-menu class="menuClass" :pageIndex="pageIndex"></cli-menu>

        <div class="bodyDiv">
            <position :positionName="position.name" :have-back="false" @positionBack="clickBack" style="font-size: 22px"></position>

            <div v-show="subTabIndex === 0">
                <el-tabs type="border-card" style="margin-top: 20px">
                    <el-tab-pane label="新增老人">
                        <el-form :model="old_info" :rules="addRule" ref="old_info" :label-position="labelPosition">



                            <div style="margin-top: 15px; margin-left: 50px; width: 100%;" class="display-row">
                                <div class="filelabel2 row-left" style="margin-top: 5px; width: 150px"><p>姓名:</p></div>
                                <el-form-item class="titleinput2 row-right" style=" margin-right:70px;width:220px;" >
                                    <el-input placeholder="姓名" v-model="old_info.Ausername"  @keyup.enter.native="submitForm('old_info')"></el-input>
                                </el-form-item>
                                <div style="color: red; margin-left: 10px; margin-top: 7px; font-size: 22px ;margin-right:30px" ><p>*</p></div>
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>健康状态:</p></div>
                                <el-form-item class="titleinput row-right"  style=" margin-right:70px;width:220px;" prop="state">
                                    <el-input placeholder="健康状态" v-model="old_info.state"></el-input>
                                </el-form-item>
                                <div style="color: red; margin-left: 10px; margin-top: 7px; font-size: 22px ;margin-right:30px" ><p>*</p></div>

                            </div>

                            <div style="margin-top: 15px; margin-left: 50px;" class="display-row">
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>性别:</p></div>
                                <el-form-item class="titleinput row-right"  style=" margin-right:70px;width:220px;" prop="gender">
                                    <el-radio v-model="old_info.gender" label="1">男</el-radio>
                                    <el-radio v-model="old_info.gender" label="2">女</el-radio>
                                </el-form-item>
                                <div style="color: red; margin-left: 10px; margin-top: 7px; font-size: 22px ;margin-right:30px" ><p>*</p></div>
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>联系电话:</p></div>
                                <el-form-item class="titleinput row-right" style=" margin-right:70px;width:220px;" prop="phone">
                                    <el-input placeholder="联系电话" v-model="old_info.phone"></el-input>
                                </el-form-item>
                                <div style="color: red; margin-left: 10px; margin-top: 7px; font-size: 22px ;margin-right:30px" ><p>*</p></div>
                            </div>

                            <div style="margin-top: 15px; margin-left: 50px;" class="display-row">
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>身份证号:</p></div>
                                <el-form-item class="titleinput row-right"  style=" margin-right:70px;width:220px;" prop="id_card">
                                    <el-input placeholder="身份证号" v-model="old_info.id_card"></el-input>
                                </el-form-item>
                                <div style="color: red; margin-left: 10px; margin-top: 7px; font-size: 22px ;margin-right:30px" ><p>*</p></div>
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>生日:</p></div>
                                <el-form-item class="titleinput row-right" style=" margin-right:70px;width:220px;" prop="birthday">
                                    <el-date-picker placeholder="生日" type="datetime" v-model="old_info.birthday" value-format="timestamp">></el-date-picker>
                                </el-form-item>
                                <div style="color: red; margin-left: 10px; margin-top: 7px; font-size: 22px ;margin-right:30px" ><p>*</p></div>
                            </div>

                            <div style="margin-top: 15px; margin-left: 50px;" class="display-row">
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>入院时间:</p></div>
                                <el-form-item class="titleinput row-right"  style=" margin-right:70px;width:220px;" prop="checkin_date">
                                    <el-date-picker placeholder="入院时间" type="datetime" v-model="old_info.checkin_date" value-format="timestamp">></el-date-picker>
                                </el-form-item>
                                <div style="color: red; margin-left: 10px; margin-top: 7px; font-size: 22px ;margin-right:30px" ><p>*</p></div>
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>出院时间:</p></div>
                                <el-form-item class="titleinput row-right" style=" margin-right:70px;width:220px;" prop="checkout_date">
                                    <el-date-picker placeholder="出院时间" type="datetime" v-model="old_info.checkout_date" value-format="timestamp">></el-date-picker>
                                </el-form-item>
                            </div>



                            <div style="margin-top: 15px; margin-left: 50px;" class="display-row">
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>房间号:</p></div>
                                <el-form-item class="titleinput row-right"  style=" margin-right:70px;width:220px;" prop="room_number">
                                    <el-input placeholder="房间号" v-model="old_info.room_number"></el-input>
                                </el-form-item>
                                <div style="color: red; margin-left: 10px; margin-top: 7px; font-size: 22px ;margin-right:30px" ><p>*</p></div>
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>照片:</p></div>
                                <div class="titleinput row-right" style=" margin-right:70px;width:220px;" prop="imgset_dir">
                                    <!--  <button v-on:click="getType">打开摄像头</button>
                                      <img :src ="video">   -->
                                    <el-input placeholder="照片" v-model="old_info.imgset_dir"></el-input>
                                </div>

                            </div>

                            <div style="margin-top: 15px; margin-left: 50px;" class="display-row">
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>主页头象:</p></div>
                                <el-form-item class="titleinput row-right"  style=" margin-right:70px;width:220px;" prop="profile_photo">
                                    <el-upload class="upload-demo"
                                               v-model="old_info.profile_photo"
                                               action="https://jsonplaceholder.typicode.com/posts/"
                                               :on-preview="handlePreview"
                                               :on-remove="handleRemove"
                                               :before-remove="beforeRemove"
                                               multiple
                                               :limit="3"
                                               :on-exceed="handleExceed"
                                               :file-list="fileList">
                                        <el-button size="small" type="primary">点击上传</el-button>
                                        <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
                                    </el-upload>
                                </el-form-item>
                                <div style="color: red; margin-left: 10px; margin-top: 7px; font-size: 22px ;margin-right:30px" ><p>*</p></div>
                            </div>

                            <div style="margin-top: 15px; margin-left: 50px;" class="display-row">
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>第一监护人姓名:</p></div>
                                <div class="titleinput row-right"  style=" margin-right:70px;width:220px;">
                                    <el-input placeholder="第一监护人姓名" v-model="old_info.name1"></el-input>
                                </div>
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>与第一监护人关系:</p></div>
                                <div class="titleinput row-right" style=" margin-right:70px;width:220px;">
                                    <el-input placeholder="与第一监护人关系" v-model="old_info.relation1"></el-input>
                                </div>
                            </div>

                            <div style="margin-top: 15px; margin-left: 50px;" class="display-row">
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>第一监护人电话:</p></div>
                                <div class="titleinput row-right"  style=" margin-right:70px;width:220px;">
                                    <el-input placeholder="第一监护人电话" v-model="old_info.phone1"></el-input>
                                </div>
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>第一监护人微信:</p></div>
                                <div class="titleinput row-right" style=" margin-right:70px;width:220px;">
                                    <el-input placeholder="第一监护人微信" v-model="old_info.wx1"></el-input>
                                </div>
                            </div>

                            <div style="margin-top: 15px; margin-left: 50px;" class="display-row">
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>第二监护人姓名:</p></div>
                                <div class="titleinput row-right"  style=" margin-right:70px;width:220px;">
                                    <el-input placeholder="第二监护人姓名" v-model="old_info.name2"></el-input>
                                </div>
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>与第二监护人关系:</p></div>
                                <div class="titleinput row-right" style=" margin-right:70px;width:220px;">
                                    <el-input placeholder="与第二监护人关系" v-model="old_info.relation2"></el-input>
                                </div>
                            </div>

                            <div style="margin-top: 15px; margin-left: 50px;" class="display-row">
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>第二监护人电话:</p></div>
                                <div class="titleinput row-right" style=" margin-right:70px;width:220px;">
                                    <el-input placeholder="第二监护人电话" v-model="old_info.phone2"></el-input>
                                </div>
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>第二监护人微信:</p></div>
                                <div class="titleinput row-right" style=" margin-right:70px;width:220px;">
                                    <el-input placeholder="第二监护人微信" v-model="old_info.wx2"></el-input>
                                </div>
                            </div>

                            <div style="margin-top: 15px; margin-left: 50px;" class="display-row">
                                <div class="filelabel row-left" style="margin-top: 5px; width: 150px"><p>情况简介:</p></div>
                                <div class="titleinput row-right" style=" margin-right:70px;width:220px;">
                                    <el-input placeholder="情况简介"  type="textarea"
                                              :autosize="{ minRows: 2, maxRows: 4}" v-model="old_info.des"></el-input>
                                </div>
                            </div>

                            <el-button size="mid" class="submitBtn" type="primary" style="margin-left: 200px; margin-top: 30px;width:100px;" @click="submitForm('old_info')">确认添加</el-button>

                            <el-button size="mid" type="primary" style="margin-left: 400px; margin-top: 30px;width:100px;" @click="back()">返回</el-button>
                        </el-form>
                    </el-tab-pane>


                </el-tabs>
            </div>
        </div>


    </div>
</template>

<script>
    import CliTitle from "../../../components/base/cliTitle";
    import CliMenu from "../../../components/base/cliMenu";
    import Position from "../../../components/base/position";
    import Cli_sub_title from "../../../components/base/cli_sub_title";
    import Notify_edit from "../../../components/notify/notify_edit";
    import DataEdit from "../../../components/message/message_edit";
    import Read_list from "../../../components/message/unread_list";

    import API from "../../../api"
    import Cookies from "js-cookie";
    import axios from "axios";
    import qs from "qs";

    export default {
        name: "admin_detail",
        components: { Read_list, DataEdit, Notify_edit, Cli_sub_title, Position, CliMenu, CliTitle},
        data(){
            return {
                name:'Video1',
                radio: '1',
                labelPosition: 'left',
                position: {
                    name: '  ',
                    haveBack: true,
                },

                pageIndex: "3",
                old_info:  {
                    type:'1',
                    Ausername:'ss',
                    state:'ss',
                    gender:'ss',
                    phone:'ss',
                    id_card:'ss',
                    birthday:'ss',
                    checkin_date:'ss',
                    checkout_date:'ss',
                    room_number:'ss',
                    imgset_dir :'ss',
                    profile_photo:'ss',
                    name1:'ss',
                    relation1:'ss',
                    phone1:'ss',
                    wx1:'ss',
                    name2:'ss',
                    relation2:'ss',
                    phone2:'ss',
                    wx2:'ss',
                    des:'ss',

                },
                position_list: {},
                subTabIndex: 0,

                user_type: Cookies.get('type'),
                loadingAdd: false,
                addRule:{
                    Ausername: [
                        { required: true, message: '请输入老人姓名', trigger: 'blur' }
                        //{ min: 3, max: 10, message: '长度在 3 到 16 个字符', trigger: 'blur' }
                    ],
                    state:[
                        { required: true, message: '请输入老人身体状况', trigger: 'blur' }
                        //{ min: 3, max: 10, message: '长度在 3 到 16 个字符', trigger: 'blur' }
                    ],
                    gender:[
                        { required: true, message: '请输入老人性别', trigger: 'blur' }
                        //{ min: 3, max: 10, message: '长度在 3 到 16 个字符', trigger: 'blur' }
                    ],
                    phone:[
                        { required: true, message: '请输入老人电话号', trigger: 'blur' }
                        //{ min: 3, max: 10, message: '长度在 3 到 16 个字符', trigger: 'blur' }
                    ],
                    id_card:[
                        { required: true, message: '请输入老人身份证号', trigger: 'blur' }
                        //{ min: 3, max: 10, message: '长度在 3 到 16 个字符', trigger: 'blur' }
                    ],
                    birthday:[
                        { required: true, message: '请输入老人生日', trigger: 'blur' }
                        //{ min: 3, max: 10, message: '长度在 3 到 16 个字符', trigger: 'blur' }
                    ],
                    checkin_date:[
                        { required: true, message: '请输入老人入住时间', trigger: 'blur' }
                        //{ min: 3, max: 10, message: '长度在 3 到 16 个字符', trigger: 'blur' }
                    ],
                    checkout_date:[
                        { required: true, message: '请输入老人离开时间', trigger: 'blur' }
                        //{ min: 3, max: 10, message: '长度在 3 到 16 个字符', trigger: 'blur' }
                    ],
                    room_number:[
                        { required: true, message: '请输入老人房间号', trigger: 'blur' }
                        //{ min: 3, max: 10, message: '长度在 3 到 16 个字符', trigger: 'blur' }
                    ],

                    profile_photo:[
                        { required: true, message: '请上传头像', trigger: 'blur' }
                        //{ min: 3, max: 10, message: '长度在 3 到 16 个字符', trigger: 'blur' }
                    ]

                },
            }
        },


        mounted() {

        },

        methods:{
            submitForm(old_info){
                this.$refs[old_info].validate((valid) => {
                    if (!valid) {
                        return
                    }
                    this.loadingAdd = true
                });
                if(this.old)

                axios.post('http://192.168.96.130:5050/api/oldperson/add', qs.stringify({
                    // request.form["username"],
                    // request.form["gender"],
                    // request.form["phone"],
                    // request.form["id_card"],
                    // request.form["birthday"],
                    // request.form["checkin_date"],
                    // request.form["checkout_date"],
                    // request.form["imgset_dir"],
                    // request.form["profile_photo"],
                    // request.form["room_number"],
                    // request.form["firstguardian_name"],
                    // request.form["firstguardian_relationship"],
                    // request.form["firstguardian_phone"],
                    // request.form["firstguardian_wechat"],
                    // request.form["secondguardian_name"],
                    // request.form["secondguardian_relationship"],
                    // request.form["secondguardian_phone"],
                    // request.form["secondguardian_wechat"],
                    // request.form["health_state"],
                    // request.form["DESCRIPTION"],
                    // request.form["ISACTIVE"],
                    // request.form["CREATED"],
                    // request.form["CREATEBY"],
                    // request.form["UPDATED"],
                    // request.form["UPDATEBY"],
                    // request.form["REMOVE"])
                    username: this.old_info.Ausername,
                    health_state:this.old_info.state,
                    gender:this.old_info.gender,
                    phone:this.old_info.phone,
                    id_card:this.old_info.id_card,
                    birthday:this.old_info.birthday,
                    checkin_date:this.old_info.checkin_date,
                    checkout_date:this.old_info.checkout_date,
                    room_number:this.old_info.room_number,
                    imgset_dir :this.old_info.imgset_dir,
                    profile_photo:this.old_info.profile_photo,
                    firstguardian_name:this.old_info.name1,
                    firstguardian_relationship:this.old_info.relation1,
                    firstguardian_phone:this.old_info.phone1,
                    firstguardian_wechat:this.old_info.wx1,
                    secondguardian_name:this.old_info.name2,
                    secondguardian_relationship:this.old_info.relation2,
                    secondguardian_phone:this.old_info.phone2,
                    secondguardian_wechat:this.old_info.wx2,
                    DESCRIPTION:this.old_info.des,
                    ISACTIVE:'',
                    CREATED:new Date(),
                    CREATEBY:1,
                    UPDATED:new Date(),
                    UPDATEBY:1,
                    REMOVE:'',

                })).then(successResponse=>{
                    if (successResponse.data.code === 'successfully') {
                        this.loadingAdd = false
                        this.$router.push({path: `/old`})
                    } else if (successResponse.data.code === 'ERROR') {
                        console.log(successResponse.data.code)
                        this.loadingAdd = false
                        alert('出现系统错误！')
                        return
                    }else {
                        console.log(successResponse.data.code)
                        return
                    }

                })
            },


            // 切换子标题
            changeTab(msg) {
                this.subTabIndex = msg.paperClaim;
            },
            // 点击返回按钮
            clickBack(){
                alert('返回')
            },
            back(){
                this.$router.push({ path:'/old'  })
            },
            getType(){
                this.video='http:/192.168.96.130:5050/api/video1/'+this.old_info.type+'/'+this.old_info.username
            },

        }

    }
</script>

<style scoped>
    @import "../../../assets/css/page/normalLayout.css";

    .display-row {
        display: -webkit-flex; /* Safari */
        -webkit-justify-content: flex-start; /* Safari 6.1+ */
        display: flex;
        justify-content: flex-start;
        width: 100%;
    }

    .row-left {
        width: 6%;
    }

    .row-right{
        width: 20%;
    }
</style>
