<template>
  <v-card>
      <v-flex xs12 sm10>
        <v-tree url="/item/category/list"
                ref="tree"
                :isEdit="isEdit"
                @handleAdd="handleAdd"
                @handleEdit="handleEdit"
                @handleDelete="handleDelete"
                @handleClick="handleClick"
        />
      </v-flex>
  </v-card>
</template>

<script>
  export default {
    name: "category",
    data() {
      return {
        isEdit:true
      }
    },
    methods: {
      handleAdd(node) {
        console.log("add .... ");
        console.log(node);
        let param = new Object();
        param = node;
        // param.parentId = node.parentId;
        // param.name = node.name;
        this.$http.post(
            "http://api.zzb.com/api/item/category/addCategory",
            param,
          )
          .then((res) => {
            if(res.code == 200){
              this.$refs.tree.getData();
            }
          })
          .catch((error) => {});
      },
      handleEdit(id, name) {
        let param = new Object();
        param.id = id;
        param.name = name;
        this.$http.post(
          "http://api.zzb.com/api/item/category/editCategory",
          param,
        )
          .then((res) => {
            console.log(res)
          })
          .catch((error) => {});
      },
      handleDelete(id) {
        let param = new Object();
        param.id = id;
        this.$http.post(
          "http://api.zzb.com/api/item/category/delCategory",
          param,
        )
          .then((res) => {
            console.log(res)
          })
          .catch((error) => {});
      },
      handleClick(node) {
        console.log(node)
      }
    }
  };
</script>

<style scoped>

</style>
