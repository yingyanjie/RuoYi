<template>
  <div class="app-container">
    <el-form :modal="form" label-width="100px">
      <el-row>
        <el-col :span="6">
          <el-form-item label="表单1" size="small">
            <el-input placeholder="请输入" v-model="form.input1"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="6">
          <el-form-item label="表单2" size="small">
            <el-input placeholder="请输入" v-model="form.input2"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="6">
          <el-form-item label="表单3" size="small">
            <el-input placeholder="请输入" v-model="form.input3"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="6">
          <el-form-item label="表单1" size="small">
            <el-input placeholder="请输入" v-model="form.input4"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
    </el-form>
  </div>
</template>

<script>
  export default {
    name: 'customerModal',
    props: {
      type : {
        type : String,
        default: 'add'
      },
      callbackData: {
        type : Object,
        default: {}
      }
    },
    data() {
      return {
        form: {
          input1: '',
          input2: '',
          input3: '',
          input4: ''
        }
      }
    },
    methods: {
      init() {
        this.form = {

        }
      },
      callback() {

      }
    }
  }
</script>

<style scoped>

</style>
