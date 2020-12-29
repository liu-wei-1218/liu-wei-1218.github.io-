<template>
  <div v-show="isediting">
    <el-dialog
      title="提示"
      :visible.sync="isediting"
      width="90%"
      :before-close="closeEditWindow"
    >
      <el-form
        :model="ruleForm"
        ref="ruleForm"
        label-width="120px"
        class="demo-ruleForm"
      >
        <el-form-item
          label="FirstName"
          prop="firstname"
          :rules="[
            {
              required: true,
              message: 'FirstName不能为空',
              trigger: ['blur', 'change'],
            },
            { min: 2, max: 15, message: 'FirstName长度介于2-15之间' },
          ]"
        >
          <el-input v-model="ruleForm.firstname" id="editfirstname"></el-input>
        </el-form-item>

        <el-form-item
          label="LastName"
          prop="lastname"
          :rules="[
            { required: true, message: 'LastName不能为空', trigger: 'blur' },
            { min: 2, max: 15, message: 'LastName长度介于2-15之间' },
          ]"
        >
          <el-input v-model="ruleForm.lastname" id="editlastname"></el-input>
        </el-form-item>

        <el-form-item
          label="Phone"
          prop="phone"
          :rules="[
            { required: true, message: '请输入手机号', trigger: 'blur' },
            {
              min: 11,
              max: 11,
              message: '手机号长度为11位',
              trigger: 'blur',
            },
          ]"
        >
          <el-input v-model="ruleForm.phone" id="editphone"></el-input>
        </el-form-item>

        <el-form-item
          prop="email"
          label="邮箱"
          :rules="[
            { required: true, message: '请输入邮箱地址', trigger: 'blur' },
            {
              type: 'email',
              message: '请输入正确的邮箱地址',
              trigger: ['blur', 'change'],
            },
          ]"
        >
          <el-input v-model="ruleForm.email" id="editemail"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button plain @click="closeEditWindow">取 消</el-button>
        <el-button type="info" plain @click="confirmedit(ruleForm)"
          >确 定</el-button
        >
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  props: ["isediting", "editworker"],
  data() {
    return {
      finisheditworker: {
        firstname: "",
        lastname: "",
        phone: "",
        email: "",
      },
      ruleForm: this.editworker,
    };
  },
  methods: {
    closeEditWindow() {
      this.$emit("closeEditWindow");
    },

    confirmedit() {
      this.$refs.ruleForm.validate((valid) => {
        if (valid) {
          this.$confirm("此操作将永久更改信息, 是否继续?", "修改提示", {
            confirmButtonText: "确定",
            cancelButtonText: "取消",
            type: "info",
          })
            .then(() => {
              this.$message({
                type: "success",
                message: "修改成功!",
              });
              this.finisheditworker.firstname = document.getElementById(
                "editfirstname"
              ).value;
              this.finisheditworker.lastname = document.getElementById(
                "editlastname"
              ).value;
              this.finisheditworker.phone = document.getElementById(
                "editphone"
              ).value;
              this.finisheditworker.email = document.getElementById(
                "editemail"
              ).value;
              this.$emit("finisheditwindow", this.finisheditworker);
            })
            .catch(() => {
              this.$message({
                type: "error",
                message: "已取消编辑",
              });
            });
        } else {
          return false;
        }
      });
    },
  },
};
</script>

<style>
</style>