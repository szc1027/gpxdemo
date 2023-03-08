<template>
    <div>
        <h1>用户列表</h1>
        <div class="box">
            <div class="top">
                <div style="width: 300px; padding-right: 20px; ">
                    <el-input placeholder="请输入内容">
                        <el-button slot="append" icon="el-icon-search"></el-button>
                    </el-input>
                </div>
                <el-button type="primary" @click="add">添加用户</el-button>
            </div>
            <el-table :data="list" border style="width: 100%">
                <el-table-column prop="index" label="#">
                </el-table-column>
                <el-table-column prop="username" label="姓名">
                </el-table-column>
                <el-table-column prop="email" label="邮箱">
                </el-table-column>
                <el-table-column prop="mobile" label="电话">
                </el-table-column>
                <el-table-column prop="role_name" label="角色">
                </el-table-column>
                <el-table-column prop="mg_state" label="状态">
                    <el-switch v-model="this.list.mg_state" active-color="#13ce66" inactive-color="#ff4949">
                    </el-switch>
                </el-table-column>
                <el-table-column fixed="right" label="操作" width="200">
                    <template slot-scope="scope">
                        <el-button type="primary" size="mini" icon="el-icon-edit"></el-button>
                        <el-button type="danger" size="mini" @click="del(scope.$index)" icon="el-icon-delete"></el-button>
                        <el-button type="warning" size="mini" icon="el-icon-star-off"></el-button>

                    </template>
                </el-table-column>
            </el-table>

            <el-dialog title="提示" :visible.sync="dialogVisible" width="30%">
                <el-form ref="form" :model="ruleForm" label-width="80px">
                    <el-form-item label="用户名称" prop="username">
                        <el-input v-model="ruleForm.usernam"></el-input>
                    </el-form-item>
                    <el-form-item label="用户密码" prop="password">
                        <el-input v-model="ruleForm.password"></el-input>
                    </el-form-item>

                </el-form>
                <span slot="footer" class="dialog-footer">
                    <el-button @click="dialogVisible = false">取 消</el-button>
                    <el-button type="primary" @click="tj">确 定</el-button>
                </span>
            </el-dialog>
        </div>
    </div>
</template>
<script>
export default {

    data() {
        return {
            list: [],
            dialogVisible: false,
            ruleForm:[{
               
            }]
        }
    },
    computed: {

    },
    watch: {

    },
    mounted() {

    },
    created() {
        this.Getlist()
    },
    methods: {
        Getlist() {
            this.$axios.get('./data.json').then(( {data}) => {
                console.log(data.users);
                this.list=data.users
                
            })
        },
        add() {
            this.dialogVisible = true
        },
        tj(){
            this.list.push(this.ruleForm)
        },
        del(i){
            this.list.splice(i,1)
        },
        handleClose(done) {
            this.$confirm('确认关闭？')
                .then(_ => {
                    done();
                })
                .catch(_ => { });
        }

    }
};
</script>
<style lang='scss' scoped>
.box {
    width: 96%;
    height: 600px;
    padding: 20px;
    background-color: #fff;

    .top {
        display: flex;

    }
}
</style>