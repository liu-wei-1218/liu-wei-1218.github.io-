<template>
  <div v-show="isdetailing">
    <el-dialog
      title="提示"
      :visible.sync="isdetailing"
      width="90%"
      :before-close="closeDetailWindow"
    >
      <el-form
        :label-position="labelPosition"
        label-width="120px"
      >
        <el-form-item label="Firstname">
          <el-input v-model="worker.firstname" readonly="readonly"></el-input>
        </el-form-item>
        <el-form-item label="Lastname">
          <el-input v-model="worker.lastname" readonly="readonly"></el-input>
        </el-form-item>
        <el-form-item label="PhoneNumber">
          <el-input v-model="worker.phone" readonly="readonly"></el-input>
        </el-form-item>
        <el-form-item label="EmailAddress">
          <el-input v-model="worker.email" readonly="readonly"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button plain @click="closeDetailWindow">取 消</el-button>
        <el-button type="info" plain @click="openedit">编 辑</el-button>
      </span>
    </el-dialog>
    <edit
      :editworker="editworker"
      :isediting="isediting"
      @closeEditWindow="closeedit"
      @finisheditwindow="setworkerdetail"
      @edit-confirm="confirmedit"
    ></edit>
  </div>
</template>

<script>
import Edit from "./Edit.vue";
export default {
  components: { Edit },
  props: ["isdetailing", "worker"],
  data() {
    return {
      isediting: false,
      editworker: this.worker,
      labelPosition: 'right',
    };
  },
  methods: {
    confirmedit(editworker){
      console.log(editworker.firstname);
    },
    closeDetailWindow() {
      this.$emit("closeDetailWindow");
    },
    openedit() {
      this.isediting = true;
    },
    closeedit() {
      this.isediting = false;
      this.$emit("closeDetailWindow");
    },
    setworkerdetail(finisheditworker) {
      this.isediting = false;
      this.$emit("setworker", finisheditworker);
    },
  },
};
</script>

<style>
</style>