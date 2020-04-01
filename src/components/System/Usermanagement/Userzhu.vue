<template>
  <div class="userzhu">
    <strong>编辑角色</strong>
    <el-divider></el-divider>
    <el-form ref="form" :model="form" label-width="80px">
      <el-form-item label="角色名称" required>
        <el-input v-model="form.name"></el-input>
      </el-form-item>
      <el-form-item label="角色类型" required>
        <el-select v-model="form.region" placeholder="请选择活动区域">
          <el-option label="区域一" value="shanghai"></el-option>
          <el-option label="区域二" value="beijing"></el-option>
          <el-option label="区域三" value="jiangxi"></el-option>
          <el-option label="区域四" value="zhejiang"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="角色描述">
        <el-input type="textarea" v-model="form.desc"></el-input>
      </el-form-item>
      <el-form-item label="功能权限" required>
        <el-tree
          :data="data"
          show-checkbox
          node-key="id"
          :default-expanded-keys="[2, 3]"
          :default-checked-keys="[5]"
          :props="defaultProps"
        >
        </el-tree>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      form: {
        name: "",
        region: "",
        desc: ""
      },
      data: [
        {
          id: 1,
          label: "一级 1",
          children: [
            {
              id: 4,
              label: "二级 1-1",
              children: [
                {
                  id: 9,
                  label: "三级 1-1-1"
                },
                {
                  id: 10,
                  label: "三级 1-1-2"
                }
              ]
            }
          ]
        },
        {
          id: 2,
          label: "一级 2",
          children: [
            {
              id: 5,
              label: "二级 2-1"
            },
            {
              id: 6,
              label: "二级 2-2"
            }
          ]
        },
        {
          id: 3,
          label: "一级 3",
          children: [
            {
              id: 7,
              label: "二级 3-1"
            },
            {
              id: 8,
              label: "二级 3-2"
            }
          ]
        }
      ],
      defaultProps: {
        children: "children",
        label: "label"
      }
    };
  }
};
</script>
<style lang="less">
.userzhu {
  margin-top: 30px;
  strong {
    font: 24px solid black;
    font-weight: bold;
  }
}
</style>
