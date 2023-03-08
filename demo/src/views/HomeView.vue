<template>
  <div>
    <div class="box">
      <h2>电商后台管理系统</h2>
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
        <el-form-item label="用户名称" prop="username">
          
          <el-input   v-model="ruleForm.username"><i slot="prefix" class="el-icon-user-solid"></i></el-input>
        </el-form-item>
        <el-form-item label="用户密码" prop="password">
          <el-input v-model="ruleForm.password"><i slot="prefix" class="el-icon-data-analysis"></i></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm')">登录</el-button>
          <el-button @click="resetForm('ruleForm')">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>
<script>

export default {
  data() {
    return {
      ruleForm:{
        username:'',
        password:''
      },
      rules: {
          username: [
            { required: true, message: '请输入用户名称', trigger: 'blur' },
            { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
          ],
          password: [
            { required: true, message: '请输入用户密码', trigger: 'blur' },
            { min: 3, max: 6, message: '长度在 3 到 6 个字符', trigger: 'blur' }
          ],
        }
    }
  },
  computed: {

  },
  watch: {

  },
  mounted() {

  },
  methods: {
    submitForm(){
      this.$axios.post('http://www.ysqorz.top:8888/api/private/v1/login').then((data)=>{
        console.log(data);
        this.$router.push('./user')
      })
    }
  }
};
</script>
<style lang='scss' scoped>
.box{
  width: 600px;
  height: 300px;
  background-color: #fff;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 20px;
  text-align: center;
}

</style>