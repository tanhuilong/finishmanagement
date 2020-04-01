<template>
  <div class="zhu">
    <div class="mid">
      <el-form :inline="true">
        <el-form-item label=" 角色类型:">
          <el-input
            size="mini"
            clearable
            placeholder="请选择"
            suffix-icon="el-icon-d-caret"
            v-model="input1"
          >
          </el-input>
        </el-form-item>
        <el-form-item label="用户姓名:">
          <el-input
            size="mini"
            clearable
            placeholder="请输入"
            suffix-icon="el-icon-d-caret"
            v-model="input2"
          >
          </el-input
        ></el-form-item>
        <el-form-item>
          <el-button type="danger" size="mini" @click="open1">
            查询
          </el-button></el-form-item
        >
        <el-form-item>
          <el-button plain size="mini" @click="dialogVisible = true">
            导出
          </el-button>
          <el-dialog
            title="选择用户"
            :visible.sync="dialogVisible"
            center
            width="1000px"
          >
            <el-container>
              <el-aside width="200px">Aside</el-aside>
              <el-container>
                <el-header
                  ><el-input placeholder="请输入内容" v-model="input3">
                    <el-button
                      slot="append"
                      icon="el-icon-search"
                      size="mini"
                    ></el-button> </el-input
                ></el-header>
                <el-main>
                  <el-transfer
                    filterable
                    :filter-method="filterMethod"
                    filter-placeholder="请输入城市拼音"
                    v-model="value"
                    :data="data"
                  >
                  </el-transfer>
                </el-main>
                <el-footer>
                  <el-input type="textarea" autocomplete="off"></el-input>
                </el-footer>
              </el-container>
            </el-container>
            <span slot="footer" class="dialog-footer">
              <el-button @click="dialogVisible = false">取 消</el-button>
              <el-button type="danger" @click="dialogVisible = false"
                >确 定</el-button
              >
            </span>
          </el-dialog></el-form-item
        >
        <el-form-item>
          <el-button
            type="danger"
            @click="dialogFormVisible = true"
            size="mini"
          >
            新增用户
          </el-button>
          <el-dialog
            title="用户设置"
            style="width:1000px;"
            :visible.sync="dialogFormVisible"
            center
          >
            <el-form :model="form">
              <el-form-item
                label="角色名称"
                label-width="80px"
                :inline="true"
                required
              >
                <el-input v-model="form.role" autocomplete="off"></el-input>
              </el-form-item>
              <el-form-item
                label="用户姓名"
                label-width="80px"
                size="medium"
                :inline="true"
                required
              >
                <el-input
                  type="textarea"
                  v-model="form.name"
                  autocomplete="off"
                ></el-input>
              </el-form-item>
              <el-button type="danger" size="mini" style="float:right;">
                选择用户
              </el-button>
            </el-form>
            <div slot="footer" class="dialog-footer">
              <el-button @click="dialogFormVisible = false" size="mini"
                >取 消</el-button
              >
              <el-button
                type="danger"
                @click="dialogFormVisible = false"
                size="mini"
                >确 定</el-button
              >
            </div>
          </el-dialog></el-form-item
        >
      </el-form>
    </div>
    <div class="z-main">
      <lie></lie>
    </div>
  </div>
</template>
<script>
import lie from "./Rolelie.vue";
export default {
  components: {
    lie
  },
  data() {
    const generateData = _ => {
      console.log(_);
      const data = [];
      const cities = ["上海", "北京", "广州", "深圳", "南京", "西安", "成都"];
      const pinyin = [
        "shanghai",
        "beijing",
        "guangzhou",
        "shenzhen",
        "nanjing",
        "xian",
        "chengdu"
      ];
      cities.forEach((city, index) => {
        data.push({
          label: city,
          key: index,
          pinyin: pinyin[index]
        });
      });
      return data;
    };
    return {
      input1: "",
      input2: "",
      input3: "",
      dialogFormVisible: false,
      dialogVisible: false,
      form: {
        name: "",
        role: ""
      },
      formLabelWidth: "120px",
      data: generateData(),
      value: [],
      filterMethod(query, item) {
        return item.pinyin.indexOf(query) > -1;
      }
    };
  },
  methods: {
    open1() {
      this.$prompt("你好", "啊哈", item => {
        if (item) {
          this.$router.replace("/new");
        }
      });
    },
    open2() {
      this.$notify({
        title: "导出",
        message: "文件"
      });
    }
  }
};
</script>
<style lang="less">
.zhu {
  .mid {
    padding-top: 20px;
    padding-left: 5px;
    background: #f5efef;
  }
  .el-form-item {
    padding-top: 10px;
  }
  .el-container {
    .el-container {
      .el-header {
        background: transparent;
      }
    }
    .el-aside {
      background: #f5f5f5;
    }
  }
  .el-dialog {
    .el-button {
      margin-top: 20px;
    }
  }
}
</style>
