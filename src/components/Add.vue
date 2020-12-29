<template>
  <div v-show="isadding">
    <el-dialog
      title="新增信息"
      :visible.sync="isadding"
      width="90%"
      :before-close="closeadd"
    >
      <el-form
        :model="ruleForm"
        :rules="rules"
        ref="ruleForm"
        label-width="120px"
        class="demo-ruleForm"
      >
        <el-form-item label="FirstName" prop="addfirstname">
          <el-input
            v-model="ruleForm.addfirstname"
            id="addfirstname"
          ></el-input>
        </el-form-item>
        <el-form-item label="LastName" prop="addlastname">
          <el-input v-model="ruleForm.addlastname" id="addlastname"></el-input>
        </el-form-item>
        <el-form-item label="Phone" prop="addphone">
          <el-input v-model="ruleForm.addphone" id="addphone"></el-input>
        </el-form-item>
        <el-form-item
          prop="addemail"
          label="邮箱"
          :rules="[
            { required: true, message: '请输入邮箱地址', trigger: 'blur' },
            {
              type: 'email',
              message: '请输入正确的邮箱地址',
              trigger: 'blur,change',
            },
          ]"
        >
          <el-input v-model="ruleForm.addemail" id="addemail"></el-input>
        </el-form-item>
      </el-form>

      <el-button @click="closeadd">取 消</el-button>
      <el-button type="primary" @click="confirmadd()">确 定</el-button>
    </el-dialog>
  </div>
</template>

<script>
export default {
  props: ["isadding"],
  data() {
    return {
      ruleForm: {
        addfirstname: "",
        addlastname: "",
        addphone: "",
        addemail: "",
      },
      rules: {
        addfirstname: [
          { required: true, message: "请输入FirstName", trigger: "blur" },
          {
            min: 1,
            max: 15,
            message: "长度在 1 到 15 个字符",
            trigger: "blur",
          },
        ],
        addlastname: [
          { required: true, message: "请输入LastName", trigger: "blur" },
          {
            min: 2,
            max: 15,
            message: "长度在 2 到 15 个字符",
            trigger: "blur",
          },
        ],
        addphone: [
          { required: true, message: "请输入PhoneNumber", trigger: "blur" },
          {
            min: 11,
            max: 11,
            message: "长度为11位",
            trigger: "blur",
          },
        ],
      },
      newworker: {
        firstname: "",
        lastname: "",
        phone: "",
        email: "",
      },
    };
  },
  methods: {
    closeadd() {
      this.initworker();
      this.$emit("closeadd");
    },
    confirmadd() {
      this.$refs.ruleForm.validate((valid) => {
        if (valid) {
          this.newworker.firstname = document.getElementById(
            "addfirstname"
          ).value;
          this.newworker.lastname = document.getElementById(
            "addlastname"
          ).value;
          this.newworker.phone = document.getElementById("addphone").value;
          this.newworker.email = document.getElementById("addemail").value;
          this.$emit("addnew", this.newworker);
          swal("Good job!", "添加成功!", "success");
          this.initworker();
        } else {
          return false;
        }
      });
    },
    initworker() {
      this.newworker = {
        firstname: "",
        lastname: "",
        phone: "",
        email: "",
      };
      document.getElementById("addfirstname").value = "";
      document.getElementById("addlastname").value = "";
      document.getElementById("addphone").value = "";
      document.getElementById("addemail").value = "";
    },
  },
};
</script>

<style>
</style>