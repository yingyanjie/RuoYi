<template>
    <div class="app-container">
        <el-card class="box-card">
            <div slot="header" class="table-header header">
                <span class="table-header-title">托盘资料</span>
                <el-input v-model="searchText" class="table-header-search" placeholder="请输入" show-word-limit maxlength="20" style="border-radius: 20%">
                    <el-button slot="append" icon="el-icon-search"></el-button>
                </el-input>
            </div>
            <!-- 按钮 -->
            <div class="button-group">
                <el-button size="small" class="add" @click="Newly_added">新增</el-button>
                <el-button size="small" class="disable">批量删除</el-button>
                <el-button size="small" class="import">导入</el-button>
            </div>
            <!-- 表格 -->
            <div class="el-table-parent">
                <el-table :data="tableData" border style="width: 100%">
                    <el-table-column label="托盘编号" prop="palletCode" align="center"></el-table-column>
                    <el-table-column label="托盘名称" prop="palletName" align="center"></el-table-column>
                    <el-table-column label="生产任务单" prop="orderNo" align="center"></el-table-column>
                    <el-table-column label="批号" prop="batchCode" align="center"></el-table-column>
                    <el-table-column label="状态" prop="dataStateName" align="center"></el-table-column>
                    <el-table-column label="操作" align="center">
                        <template slot-scope="scope">
                            <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
                            <el-button type="text" size="small">编辑</el-button>
                        </template>
                    </el-table-column>
                </el-table>
                <!-- 分页 -->
                <el-pagination class="pagePlug" :total="total" layout="total, sizes, prev, pager, next, jumper" @current-change="handleCurrentChange" @size-change="handleSizeChange" :page-sizes="[10, 20, 30, 40]" :current-page="currentPage"></el-pagination>
            </div>
        </el-card>
        <!-- 新增 -->
        <el-dialog title="新增" :visible.sync="Dialog1" width="25%" :close-on-click-modal="false">
            <el-form ref="form" :model="form" label-width="90px" :rules="rules">
                <el-form-item label="托盘编号" prop="tray_code">
                    <el-input type="text" v-model="form.tray_code" maxlength="25"></el-input>
                </el-form-item>
                <el-form-item label="托盘名称" prop="tray_name">
                    <el-input type="text" v-model="form.tray_name" maxlength="25"></el-input>
                </el-form-item>
                <el-form-item label="生产任务单">
                    <el-input type="text"v-model="form.tray_task" maxlength="25"></el-input>
                </el-form-item>
                <el-form-item label="批号">
                    <el-input type="text" v-model="form.tray_batch" maxlength="25"></el-input>
                </el-form-item>
            </el-form>
            <span slot="footer" class="dialog-footer">
                <el-button type="primary" @click="Determine(form)">确 定</el-button>
                <el-button @click="Dialog1 = false">取 消</el-button>
            </span>
        </el-dialog>
        <!-- 编辑 -->
        <el-dialog title="新增" :visible.sync="Dialog2" width="25%" :close-on-click-modal="false">
            <el-form ref="form" :model="form" label-width="90px" :rules="rules">
                <el-form-item label="托盘编号" prop="tray_code">
                    <el-input type="text" v-model="form.tray_code" maxlength="25"></el-input>
                </el-form-item>
                <el-form-item label="托盘名称" prop="tray_name">
                    <el-input type="text" v-model="form.tray_name" maxlength="25"></el-input>
                </el-form-item>
                <el-form-item label="生产任务单">
                    <el-input type="text" v-model="form.tray_task" maxlength="25"></el-input>
                </el-form-item>
                <el-form-item label="批号">
                    <el-input type="text" v-model="form.tray_batch" maxlength="25"></el-input>
                </el-form-item>
            </el-form>
            <span slot="footer" class="dialog-footer">
                <el-button type="primary" @click="Determine1">确 定</el-button>
                <el-button @click="Dialog2 = false">取 消</el-button>
            </span>
        </el-dialog>
    </div>
</template>

<script>
import '@/resources/overwrite.css'
export default {
    data () {
        return {
            total:10,   //分页总页数
            currentPage:1,   //当前页数
            Dialog1:false,  //新增弹出框
            Dialog2:false,  //编辑弹出框
            form:{
                tray_code:'',   //托盘编号
                tray_name:'',   //托盘名称
                tray_task:'',   //生产任务单
                tray_batch:'',  //批号
            },
            rules: {
                tray_code: [
                    { required: true, message: '请输入', trigger: 'blur' },
                ],
                tray_name: [
                    { required: true, message: '请输入', trigger: 'blur' },
                ]
            }
        }
    },
    methods: {
        Newly_added(){
            this.Dialog1=true

        },
        Determine(form){
            console.log(form)
        }
    },
    
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
.mast-text{
    margin-right:5px;
    color: red;
}
</style>