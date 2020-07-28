<template>
  <div>
    <el-tree :data="menus" :props="defaultProps" @node-click="handleNodeClick" :expand-on-click-node="false"
    show-checkbox node-key="catId">
      <span class="custom-tree-node" slot-scope="{ node, data }">
        <span>{{ node.label }}</span>
        <span>
          <el-button v-if="node.level<=2" type="text" size="mini" @click="() => append(data)">
            新增
          </el-button>
          <el-button v-if="node.childNodes.length==0" type="text" size="mini" @click="() => remove(node, data)">
            删除
          </el-button>
        </span>
      </span>
    </el-tree>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        menus: [],
        defaultProps: {
          children: 'children',
          label: 'name'
        }
      };
    },
    methods: {

      append(data) {
        console.log("add===", data)
      },

      remove(node, data) {
        console.log("remove===", data)
      },

      getMenus() {
        this.$http({
          url: this.$http.adornUrl('/product/category/list/tree'),
          method: 'get'
        }).then(({
          data
        }) => {
          this.menus = data.data
        })
      }
    },
    created() {
      this.getMenus();
    }
  };
</script>

<style>
</style>
