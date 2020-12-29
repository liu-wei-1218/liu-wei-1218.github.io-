<template>
  <div>
    <table class="table" border="0px">
      <thead>
        <tr>
          <td width="30%"></td>
          <td width="35%">Last Name</td>
          <td width="35%">First Name</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(worker, index) in workers" :key="index">
          <td>
            <a @click="deleteInfo(index)">删除&nbsp;&nbsp;</a>
            <a @click="details(index)">Details</a>
          </td>
          <td>{{ worker.lastname }}</td>
          <td>{{ worker.firstname }}</td>
        </tr>
        <tr>
          <td colspan="3">
            <button class="btn btn-primary" @click="openadd">Add worker</button>
            <button class="btn btn-info" @click="express()">Read me</button>
          </td>
        </tr>
      </tbody>
    </table>
    <Add
      :isadding="isadding"
      @closeadd="closeaddwindow"
      @addnew="addnewworker"
    ></Add>
    <Detail
      :isdetailing="isdetailing"
      :worker="worker"
      @closeDetailWindow="closeDetail"
      @setworker="setworkerInfo"
    ></Detail>
  </div>
</template>

<script>
import Add from "./Add.vue";
import Detail from "./Detail";
export default {
  props: ["workers"],
  components: {
    Detail,
    Add,
  },
  data() {
    return {
      isexpressing: false,
      isadding: false,
      isdetailing: false,
      worker: {
        firstname: "",
        lastname: "",
        phone: "",
        email: "",
      },
    };
  },
  methods: {
    //删除
    deleteInfo(index) {
      this.$confirm("此操作将永久删除该文件, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      })
        .then(() => {
          this.$message({
            type: "success",
            message: "删除成功!",
          });
          this.workers.splice(index, 1);
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除",
          });
        });
    },
    //查看详情
    details(index) {
      var inde = index;
      localStorage.setItem("inde", inde);
      this.worker.firstname = this.workers[index].firstname;
      this.worker.lastname = this.workers[index].lastname;
      this.worker.phone = this.workers[index].phone;
      this.worker.email = this.workers[index].email;
      this.isdetailing = true;
    },
    //关闭查看详情界面
    closeDetail(editworker) {
      this.isdetailing = false;
      // workers[inde]=editworker;
    },

    setworkerInfo(_finisheditworker) {
      // console.log("这是Infotable");
      this.isdetailing = false;
      let __finisheditworker = _finisheditworker;
      // console.log(__finisheditworker);
      // console.log(localStorage.getItem("inde"));

      this.$emit(
        "changeworker",
        __finisheditworker,
        localStorage.getItem("inde")
      );
    },
    openadd() {
      this.isadding = true;
    },
    closeaddwindow() {
      this.isadding = false;
    },
    addnewworker(newworker) {
      let _newworker = newworker;
      console.log(_newworker.firstname);
      this.workers.splice(0, 0, _newworker);
      this.isadding = false;
    },
    express() {
        swal("组件声明：Infotable组件提供workers数组,并带有2个子组件:Detail、Add,分别实现查看和新增功能,且Detail含有Edit子组件,通过Edit子组件实现编辑功能。");
    },
  },
};
</script>

<style scoped>
.btn {
  margin: auto;
}
</style>