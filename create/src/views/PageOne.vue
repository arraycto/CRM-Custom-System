<template >
    <div class="size">
        <el-table
                :data="tableData"
                border
                style="width: 100%">
            <el-table-column
                    fixed
                    prop="id"
                    label="客户编号"
                    width="120">
            </el-table-column>
            <el-table-column
                    prop="name"
                    label="客户姓名"
                    width="120">
            </el-table-column>
            <el-table-column
                    prop="source"
                    label="客户来源"
                    width="120">
            </el-table-column>
            <el-table-column
                    prop="work"
                    label="客户工作行业"
                    width="120">
            </el-table-column>
            <el-table-column
                    prop="level"
                    label="客户等级"
                    width="120">
            </el-table-column>
            <el-table-column
                    prop="tel"
                    label="联系方式"
                    width="120">
            </el-table-column>
            <el-table-column
                    prop="phone"
                    label="固定电话"
                    width="120">
            </el-table-column>
            <el-table-column
                    prop="code"
                    label="客户编码"
                    width="120">
            </el-table-column>
            <el-table-column
                    prop="address"
                    label="家庭住址"
                    width="120">
            </el-table-column>
            <el-table-column
                    fixed="right"
                    label="修改"
                    width="100">
                <template slot-scope="scope">
                    <el-button @click="edit(scope.row)" type="text" size="small"><el-button type="primary" icon="el-icon-edit" circle size="small"></el-button></el-button>
                    <el-button @click="deleteCustom(scope.row)" type="text" size="small"> <el-button type="danger" icon="el-icon-delete" circle size="small"></el-button></el-button>

                </template>

            </el-table-column>
        </el-table>
        <el-main></el-main>
        <el-pagination
                background
                layout="prev, pager, next"
                :page-size="6"
                :total="total"
                @current-change="page">
        </el-pagination>
    </div>

</template>


<script>
    export default {
        methods: {
            deleteCustom(row){
                const _this = this
              axios.delete('http://localhost:8181/custom/deleteById/'+row.id).then(function (resp) {

                    _this.$alert("用户"+row.name+"删除成功",
                  {
                      confirmButtonText:'确定',
                          callback :action =>{
                          window.location.reload()
                  }
                  })



              })
            },
            edit(row){
                this.$router.push({
                    path: '/update',
                    query:{
                        id:row.id
                    }
                })
            },
        page(currentPage)
    {
        const _this = this
        axios.get('http://localhost:8181/custom/findAll/'+currentPage+'/6').then(function (resp) {
            _this.tableData = resp.data.content
            _this.total=resp.data.totalElements
        })
    },
        },
        created() {
            const _this = this
            axios.get('http://localhost:8181/custom/findAll/1/6').then(function (resp) {
                _this.tableData = resp.data.content
                _this.total=resp.data.totalElements

            })
        },
        data() {
            return {
                total: null,
                tableData: null
            }
        }

    }
</script>

<style scoped>
/*.size{*/
/*    background-color: coral*/
/*}*/
</style>