<template>
    <div id="registered" style="">
        <div class='bg-style' style="width:100%;">
            <div class='content-left' style="float:left;width:40%;text-align: center;color:#fff;margin: 310px 120px;">
                <p style="font-size:60px;">健康中心系统</p>
                <span style="font-size:21px;font-weight:400;">
                    我们与您共同关注着您的健康状态
                </span>
            </div>

            <div class="register-form" style=""> 
                <div class="register-container" style="padding:10px;">
                    <Form ref="formValidate" :model="formValidate" :rules="ruleValidate" :label-width="90">
                        <FormItem label="名称：" prop="name">
                            <Input v-model="formValidate.name" placeholder="Enter your name" style="width:75%"></Input>
                        </FormItem>
                        <FormItem label="密码：" prop="pwd">
                            <Input v-model="formValidate.pwd" placeholder="Enter your password" style="width:75%"></Input>
                            <span style="display: block;color: #6a737d;font-size: 12px;">至少包含一个数字，字母，长度大于6</span>
                        </FormItem>
                        <FormItem label="签名：" prop="signature">
                            <Input v-model="formValidate.signature" placeholder="Enter your signature" style="width:75%"></Input>
                        </FormItem>
                        <FormItem label="邮箱：" prop="mail">
                            <Input v-model="formValidate.mail" placeholder="Enter your e-mail" style="width:75%"></Input>
                        </FormItem>
                        <FormItem label="性别：" prop="gender">
                            <RadioGroup v-model="formValidate.gender">
                                <Radio label="male">男</Radio>
                                <Radio label="female">女</Radio>
                            </RadioGroup>
                        </FormItem>
                        <FormItem label="身高：" prop="height">
                            <!--<InputNumber :min="1" v-model="formValidate.height">-->
                            <!--<span>cm</span>-->
                            <Input v-model="formValidate.height" placeholder="height" type="number" style="width:80px;"></Input>
                            <span>cm</span>
                        </FormItem>
                        <FormItem label="体重：" prop="weight">
                            <Input v-model="formValidate.weight" placeholder="weight" type="number" style="width:80px;"></Input>
                            <span>kg</span>
                            <!--<InputNumber :min="1" v-model="formValidate.weight">-->
                            <!--<span>kg</span>-->
                            <!--<Input v-model="formValidate.name" placeholder="Enter your weight"></Input>-->
                        </FormItem>
                        <FormItem label="出生日期：" prop="date">
                            <Row>
                                <Col span="11">
                                <DatePicker type="date" format="yyyy-MM-dd" placeholder="Select date" @on-change="date"></DatePicker>
                                </Col>
                                <!--<Col span="2" style="text-align: center">-</Col>-->
                            </Row>
                        </FormItem>
                        <FormItem label="血型：" prop="blood">
                            <Select v-model="formValidate.blood" placeholder="Select your blood type" style="width:80px;">
                                <Option value="A">A型</Option>
                                <Option value="B">B型</Option>
                                <Option value="AB">AB型</Option>
                                <Option value="O">0型</Option>
                            </Select>
                        </FormItem>
                        <!--<FormItem label="爱好：" prop="interest">-->
                            <!--<CheckboxGroup v-model="formValidate.interest">-->
                            <!--<Checkbox label="吃"></Checkbox>-->
                            <!--<Checkbox label="睡"></Checkbox>-->
                            <!--<Checkbox label="运动"></Checkbox>-->
                            <!--<Checkbox label="电影"></Checkbox>-->
                            <!--</CheckboxGroup>-->
                        <!--</FormItem>-->
                        <!--<FormItem>-->
                            <div style="width: 80%;margin: -15px auto;margin-bottom: 15px;">
                                <Button type="primary" long @click="handleSubmit('formValidate')">注册</Button>
                                <!--<Button @click="handleReset('formValidate')" style="margin-left: 8px">取消</Button>-->
                            </div>
                        <!--</FormItem>-->
                        <div style="text-align: center">
                            <span style="color: #6a737d;font-size: 12px;">点击“注册”即表示您同意我们 的服务条款和 隐私声明。我们偶尔会向您发送与帐户相关的电子邮件。</span>
                        </div>
                    </Form>
                </div>
            </div>
        </div>

    </div>
</template>

<script>

export default {
        name: 'forum',
        data() {


            const validateDate = (rule, value, callback, source, options) => {
                if (value === '') {
                    callback(new Error('请选择出生日期'));
                }  else {
                    callback();
                }
            };

            const validateNumber = (rule, value, callback) => {
                if (value === '') {
                    callback(new Error('不能为空'));
                } else if( value<1 ) {
                    callback(new Error('不能小于1'));
                } else {
                    callback();
                }
            };

            const validatePwd = (rule, value, callback) => {
                var reg = /^[a-zA-Z0-9_\u4e00-\u9fa5]+$/;
                if (value === '') {
                    callback(new Error('不能为空'));
                } else if(!reg.test(value)) {
                    callback(new Error('只能含有英文大小写字母、下划线、数字、中文'));
                } else if (value.length < 6) {
                    callback(new Error('至少6个字符'));
                } else if (value.length >= 35) {
                    callback(new Error('应35个字符以内'));
                } else {
                    callback();
                }
            };

            return {
               formValidate: {
                    name: '',
                    signature:'',
                    mail: '',
                   blood: '',
                    gender: 'male',
//                    interest: [],
                    date:'',
                    height:'',
                    weight:'',
//                    time: '',
                },ruleValidate: {
                    name: [
                        { required: true, message: '名称不能为空', trigger: 'blur' }
                    ],
                    pwd: [
                        { validator: validatePwd, trigger: 'blur',required: true }
                    ],
                    signature: [
                        { required: true, message: '签名不能为空', trigger: 'blur' }
                    ],
                    mail: [
                        { required: true, message: '邮箱不能为空', trigger: 'blur' },
                        { type: 'email', message: '请正确输入邮箱格式', trigger: 'blur' }
                    ],
                    blood: [
                        { required: true, message: '请选择您的血型', trigger: 'change' }
                    ],
                    gender: [
                        { required: true, message: '请选择身份', trigger: 'change' }
                    ],
                    height: [
                        {validator: validateNumber, trigger: 'number',required: true}
//                        { required: true, message: '身高不能为空', trigger: 'blur' }
                    ],
                    weight: [
                        {validator: validateNumber, trigger: 'number',required: true}
//                        { required: true, message: '体重不能为空', trigger: 'blur' }
                    ],
//                    interest: [
//                        { required: true, type: 'array', min: 1, message: '至少选择一个爱好', trigger: 'change' },
//                        { type: 'array', max: 3, message: '最多选择三个爱好', trigger: 'change' }
//                    ],
                    date: [
                        {validator: validateDate, trigger: 'blur',required: true}
//                        { required: true, type: 'date', message: '出生日期不能为空', trigger: 'change' }
                    ],
                }
            }
        },
        props:[],
        mounted() {
           
        },
        created() {
            console.log(process.env.API_ROOT);
        },
        methods: {

            date(e){
                this.formValidate.date = e;
            },
        
             handleSubmit (name) {
                this.$refs[name].validate((valid) => {
                    if (valid) {
                        this.$Message.success('注册成功！');
                        // var x = this.formValidate;
                        // // console.log(this.formValidate)
                        // this.$http.post('http://47.107.125.48:8010/api/v1_0/auth/register',{
                        //     user_name: x.name,
                        //     user_password: x.pwd,
                        //     email: x.mail,
                        //     signature: x.signature,
                        //     sex: x.gender,
                        //     height: x.height,
                        //     weight: x.weight,
                        //     birthday: x.date,                                blood: x.blood
                        // },{emulateJSON:true}).then(function(data){
                        // if(data.status === 200){
                        // this.$Message.success('注册成功！');
                        // }
                        //  console.log(data); 
                        // }).catch(function(error){
                        //     this.$Message.success('注册失败！' + error);
                        // });
                        } else {
                            this.$Message.error('请正确填写表单信息');
                        }
                    })
                },
            handleReset (name) {
                this.$refs[name].resetFields();
            }

        }
    }

</script>

<style type="text/css">

    #registered{
        position: fixed;
        width: 100%;
        height:100%;
        background:url('./../../images/3.jpg') center;
        background-size: cover;
        background-color:#2b3137;
        opacity: 0.8;
    }

    .register-form{
        float:left;
        margin-top:35px;
        margin-left:-50px;
        width: 33%;
        /*height: 460px;*/
        background:#fff;
        box-shadow: 0 0 3px #000;
        border-radius: 5px;
    }

    #registered .ivu-form-item{
        margin-bottom: 15px;
    }



</style>