<template>
  <div class="app-container">
    <el-row :gutter="20">
      <el-col :span="6" :xs="24">
        <div class="head-container">
          <el-card>
            <div slot="header" class="tree-header">
              <span class="tree-header-title">物料类别</span>
            </div>
            <div class="button-group">
              <el-button type="primary" size="small">新增</el-button>
            </div>
            <div class="el-tree-parent">
              <el-tree
                :data="materialTree"
                :props="defaultProps"
                default-expand-all></el-tree>
            </div>
          </el-card>
        </div>
      </el-col>
      <el-col :span="18" :xs="24">
        <el-card>
          <div slot="header" class="table-header header">
            <span class="table-header-title">物料信息</span>
            <el-input
              v-model="searchText"
              class="table-header-search"
              placeholder="请输入"
              show-word-limit
              maxlength="20"
              style="border-radius: 20%">
              <el-button slot="append" icon="el-icon-search"></el-button>
            </el-input>
          </div>
          <div class="button-group">
            <el-button size="small" class="add" @click="handleAdd">新增</el-button>
            <el-button size="small" class="enable">启用</el-button>
            <el-button size="small" class="disable">停用</el-button>
            <el-button size="small" class="disable">批量删除</el-button>
            <el-button size="small" class="advancedQuery">高级查询</el-button>
            <el-button size="small" class="import">导入</el-button>
          </div>
          <div class="el-table-parent">
            <el-table v-loading="loading" @selection-change="">
              <el-table-column label="列1"></el-table-column>
              <el-table-column label="列2"></el-table-column>
              <el-table-column label="列3"></el-table-column>
              <el-table-column label="列4"></el-table-column>
              <el-table-column label="列5"></el-table-column>
              <el-table-column label="列6"></el-table-column>
              <el-table-column
                label="操作"
                align="center"
                width="120"
                class-name="small-padding fixed-width"></el-table-column>
            </el-table>
            <pagination
              class="pagePlug"
              :total="total"
              :page.sync="queryParams.pageNum"
              :limit.sync="queryParams.pageSize" @pagination="getList"></pagination>
          </div>
        </el-card>
      </el-col>
    </el-row>
    <!-- 新增修改对话框 -->
    <el-dialog title="新增" :visible.sync="open" width="60vw">
      <Modal :type="modalType" ></Modal>
      <div slot="footer" class="dialog-footer">
        <el-button type="primary">保存</el-button>
        <el-button @click="open = false">取消</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
  import '@/resources/overwrite.css'
  import Modal from './modal'

  export default {
    name: 'customer',
    data() {
      return {
        // 选中数组
        ids: [],
        // 查询语句
        searchText: '',
        // 总数
        total: 10,
        // 表格分页参数
        queryParams: {
          pageNum: 1,
          pageSize: 10
        },
        // 树
        materialTree: [
          {
            label: '一级',
            children : [
              {
                label: '二级-1',
              },
              {
                label: '二级-2',
              },
              {
                label: '二级-3',
              },
            ]
          }
        ],
        // 树插件配置字段
        defaultProps : {
          children : 'children',
          label: 'label'
        },
        loading: false,
        open: false,
        modalType: 'add'
      }
    },
    components: {Modal},
    methods: {
      handleAdd() {
        this.title='新增'
        this.modalType = 'add'
        this.open = true
      },
      handleEdit() {
        this.title = '编辑'
        this.modalType = 'edit'
        this.open = true
      },
      getList() {

      },
      handleSelectionChange(selection) {

      }
    }
  }
</script>

<style scoped>
  .tree-header {
    height: 36px;
    line-height: 26px;
  }

  .table-header {
    display: inline-flex;
    justify-content: space-between;
    width: 100%;
  }

  .table-header-title {
    width: 100px;
    line-height: 26px;
  }

  .table-header-search {
    width: 15vw;
    top: -5px;
  }

  .el-tree-parent {
    height: 72vh;
  }
</style>
