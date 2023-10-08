<template>
  <div>
    <div class="form-group">
      <label for="exampleInputEmail1">title</label>
      <input
        type="text"
        class="form-control"
        id="exampleInputEmail1"
        aria-describedby="emailHelp"
        v-model="newProduct.title"
      />
    </div>
    <div class="form-group">
      <label for="">Create</label>
      <input type="date" class="form-control" v-model="newProduct.created_at" />
    </div>
    <button @click="addProduct" class="btn btn-primary">Submit</button>
    <button class="btn btn-danger" @click="$emit('close')">close</button>
  </div>
</template>


<script>
export default {
  emits: ["close"],
  data() {
    return {
      newProduct: {
        name: "",
        created_at: "",
      },
    };
  },
  methods: {
    addProduct() {
      // Gửi sự kiện thêm sản phẩm với dữ liệu mới
      this.$emit("add-product", { ...this.newProduct });
      console.log(this.newProduct);
      // Xóa dữ liệu trên form sau khi thêm sản phẩm
      this.newProduct = { name: "", created_at: "" };
    },
  },
};
</script>