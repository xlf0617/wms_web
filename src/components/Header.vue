<template>
  <div style="display: flex;line-height: 60px">
    <div style="margin-top: 8px">
      <i :class="icon" style="font-size: 24px;cursor: pointer" @click="collapse"></i>
    </div>
    <div style="flex: 1;text-align: center;font-size: 34px">
      <span>欢迎来到仓库管理系统</span>
    </div>
    <el-dropdown>
      <span style="cursor: pointer">{{user.name}}</span>
      <i class="el-icon-arrow-down" style="margin-right: 15px;margin-left: 10px"></i>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item @click.native="toUser">个人中心</el-dropdown-item>
        <el-dropdown-item @click.native="logout">退出登录</el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
  </div>
</template>

<script>
export default {
  name: "Header",
  data(){
    return {
      user:JSON.parse(sessionStorage.getItem('CurUser')),
      // json:'',
      // name:''
    }
  },
  props: {
    icon: String
  },
  methods: {
    init(){
      this.user=JSON.parse(sessionStorage.getItem('CurUser'))
      this.json=this.user[0]
      this.name=this.json.name
    },
    toUser() {
      console.log('to_user')

      this.$router.push("/Home")
    },
    logout() {
      console.log('logout')
      this.$confirm('此操作将退出账户登录, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning',
        center:true
      }).then(() => {
        this.$message({
          type: 'success',
          message: '退出登录成功!'
        });
        sessionStorage.clear()
        this.$router.push("/")
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消退出'
        });
      });

    },
    collapse() {
      this.$emit('doCollapse')
    }
  },
  beforeMount() {
    //   this.init()
    // console.log(this.user)
    // console.log(this.name)
  },
  created() {
    this.$router.push("/Home")
  }
}
</script>

<style scoped>

</style>