<template>
  <div id="app">
    <!-- 卡片组件 -->
    <el-card class="login-card">
      <!-- 登录表单 -->
      <el-form
        style="margin-top: 50px"
        :model="loginForm"
        :rules="loginRules"
        ref="loginForm"
      >
        <el-form-item prop="mobile">
          <el-input
            placeholder="请输入手机号"
            v-model="loginForm.mobile"
          ></el-input>
        </el-form-item>

        <el-form-item prop="password">
          <el-input
            placeholder="请输入密码"
            v-model="loginForm.password"
          ></el-input>
        </el-form-item>

        <el-form-item>
          <el-button type="primary" style="width: 100%" @click="login"
            >登录</el-button
          >
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    const checkMobile = function (rule, value, callback) {
      value.charAt(2) === "9"
        ? callback()
        : callback(new Error("第三位手机号必须是9"));
    };
    return {
      // 表单数据
      loginForm: {
        mobile: "13912345678",
        password: "12345678",
      },
      // 校验规则
      loginRules: {
        mobile: [
          { required: true, message: "手机号不能为空", trigger: "blur" },
          {
            pattern: /^1[3-9]\d{9}$/,
            message: "请输入正确的手机号",
            trigger: "blur",
          },
          {
            trigger: "blur",
            validator: checkMobile,
          },
        ],
        password: [
          { required: true, message: "密码不能为空", trigger: "blur" },
          {
            min: 6,
            max: 16,
            message: "密码应为6-16位的长度",
            trigger: "blur",
          },
        ],
      },
    };
  },
  methods: {
    login() {
      // this.$refs.loginForm.validate((isOK) => {
      //   if (isOK) {
      //     console.log("校验通过");
      //   }
      // });

      this.$refs.loginForm
        .validate()
        .then(() => {
          console.log("成功");
        })
        .catch(() => {
          console.log("失败");
        });
    },
  },
};
</script>


<style scoped lang="less">
#app {
  width: 100%;
  height: 100vh;
  background-color: pink;
  display: flex;
  justify-content: center;
  align-items: center;
}
.login-card {
  width: 440px;
  height: 300px;
}
</style>
