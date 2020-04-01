<template>
  <div class="new">
    <div class="multiple-table">
      <el-table :data="tableData" style="width: 100%">
        <el-table-column prop="date" label="日期" width="150">
        </el-table-column>
        <el-table-column label="配送信息">
          <el-table-column prop="name" label="姓名" width="120">
          </el-table-column>
          <el-table-column label="地址">
            <el-table-column prop="province" label="省份" width="120">
            </el-table-column>
            <el-table-column prop="city" label="市区" width="120">
            </el-table-column>
            <el-table-column prop="address" label="地址" width="300">
            </el-table-column>
            <el-table-column prop="zip" label="邮编" width="120">
            </el-table-column>
          </el-table-column>
        </el-table-column>
      </el-table>
    </div>
    <div class="move-table">
      <el-table :data="tableData" style="width: 100%" max-height="250">
        <el-table-column fixed prop="date" label="日期" width="150">
        </el-table-column>
        <el-table-column prop="name" label="姓名" width="120">
        </el-table-column>
        <el-table-column prop="province" label="省份" width="120">
        </el-table-column>
        <el-table-column prop="city" label="市区" width="120">
        </el-table-column>
        <el-table-column prop="address" label="地址" width="300">
        </el-table-column>
        <el-table-column prop="zip" label="邮编" width="120"> </el-table-column>
        <el-table-column fixed="right" label="操作" width="120">
          <template slot-scope="scope">
            <el-button
              @click.native.prevent="deleteRow(scope.$index, tableData)"
              type="text"
              size="small"
            >
              移除
            </el-button>
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    deleteRow(index, rows) {
      rows.splice(index, 1);
    }
  },

  data() {
    var _this = this;
    var url = "json/Table.json";
    this.$http.get(url).then(des => {
      _this.tableData = des.data;
    });
    return {
      tableData: []
    };
  }
};
</script>
<style lang="less">
.new{
  padding: 30px;
}
</style>
