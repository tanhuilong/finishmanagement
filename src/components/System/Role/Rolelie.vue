<template>
  <div class="lie">
    <template>
      <el-table :data="tableData" height="350" style="width: 100%">
        <el-table-column prop="num" label="序号" width="70%"> </el-table-column>
        <el-table-column prop="roleclass" label="角色类型" width="80%">
        </el-table-column>
        <el-table-column prop="rolename" label="角色名称" width="250">
        </el-table-column>
        <el-table-column prop="roledescribe" label="角色描述" width="250px">
        </el-table-column>
        <el-table-column  label="操作">
           <template slot-scope="scope" :inline="true">
             <el-button 
             type="text"
          size="mini"
          @click="handleSet(scope.$index, scope.row)"><span class="color1">用户设置</span></el-button>
        <el-button
          size="mini"
           type="text"
          @click="handleEdit(scope.$index, scope.row)"><span class="color1">编辑</span></el-button>
        <el-button
          size="mini"
           type="text"
          @click="handleDelete(scope.$index, scope.row)"><span class="color1">删除</span></el-button>
      </template>
        </el-table-column>       
      </el-table>
      <div class="l-footer">
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage4"
          :page-sizes="[100, 200, 300, 400]"
          :page-size="100"
          layout="total, sizes, prev, pager, next, jumper"
          :total="400"
        >
        </el-pagination>
      </div>
    </template>
  </div>
</template>
<script>
export default {
  data() {
    var _this = this;
    var url = "json/lei1.json";
    this.$http.get(url).then(res => {
      _this.tableData = res.data;
    });
    return {
      tableData: [],
      currentPage4: 4
    };
  },
  methods: {
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
    },
     handleSet(index, row) {
        console.log(index, row);
      },
     handleEdit(index, row) {
        console.log(index, row);
      },
      handleDelete(index, rows) {
       this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'danger'
        }).then(() => {
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
          rows.splice(index,1)
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });          
        });
      }
  }
};
</script>
<style lang="less">
.lie {
  .l-top {
    height: 40px;
    color: #fff;
    margin: 10px 0 0 10px;
  }
  .l-mid {
    margin-left: 10px;
  }
  .el-col div {
    font-size: 14px;
  }
  li {
    list-style: none;
    height: 30px;
  }
  .l-footer {
    text-align: center;
  }
  .color1{
    color:red;
  }
}
</style>
