<template>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css"
  />

  <Header></Header>
  <div class="saibar">
    <div>
      <button @click="FilterL('')" class="btn btn-outline-info">All</button>
    </div>
    <div>
      <button @click="FilterL('completed')" class="btn btn-outline-success">
        Completed
      </button>
    </div>
    <div>
      <button @click="FilterL('pending')" class="btn btn-outline-danger">
        Pending
      </button>
    </div>
  </div>
  <button @click="stt = true">add</button>
  <Form @close="closeform" v-show="stt" @add-product="addProduct" />
  <div class="main">
    <div style="margin-top: 20px">
      <!-- <Form @addProduct="addProduct" /> -->
    </div>
    <div class="tab">
      <table class="table">
        <thead>
          <th>#</th>
          <th>title</th>
          <th>rate</th>
          <th>date</th>
          <th>Action</th>
        </thead>
        <tbody>
          <tr v-for="item in filterList" :key="item.id">
            <td></td>
            <td>{{ item.title }}</td>
            <td>
              <button @click="vt = true">
                {{ rateToStars }}
                <RateVue @cancel="dong" v-show="vt" />
              </button>
            </td>
            <td>{{ item.created_at }}</td>
            <td style="display: flex; margin: auto">
              {{ item.status }}
              <div style="margin-right: 10px" class="form-check">
                <input
                  class="form-check-input"
                  type="checkbox"
                  id="flexCheckChecked"
                  checked
                  v-model="item.status"
                />
              </div>
              <div>
                <button @click="xoa(item.id)" style="border: none">
                  <i class="fa-solid fa-trash" style="color: #0fcde6"></i>
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <button @click="removeAll" style="color: #0fcde6; margin-top: 50px">
      Clear All <i class="fa-solid fa-trash" style="color: #0fcde6"></i>
    </button>
  </div>
</template>

<script>
import FormVue from "./components/Form.vue";
import HeaderVue from "./components/Header.vue";
import RateVue from "./components/Rate.vue";
export default {
  name: "App",
  components: {
    Header: HeaderVue,
    Form: FormVue,
    Rate: RateVue,
  },
  data() {
    return {
      vt: false,
      stt: false,
      list: "all",
      products: [
        {
          id: 1,
          title: "iphone",
          rate: 1,
          created_at: "9-2-2012",
          status: false,
        },
        {
          id: 2,
          title: "samsung",
          rate: 1,
          created_at: "9-2-2012",
          status: false,
        },
      ],
    };
  },
  computed: {
    filterList() {
      // Tạo danh sách sản phẩm dựa trên trạng thái filter
      if (this.list === "pending") {
        return this.products.filter((item) => !item.status); // Lọc sản phẩm có status là false
      } else if (this.list === "completed") {
        return this.products.filter((item) => item.status); // Lọc sản phẩm có status là true
      } else {
        return this.products; // Hiển thị tất cả sản phẩm khi filter là "all"
      }
    },

    rateToStars() {
      const rate = this.products.rate; // Lấy giá trị rate từ item
      // Logic chuyển đổi rate thành biểu tượng ngôi sao
      // Ví dụ: rate 4.5 sẽ trở thành "★★★★☆"
      const stars =
        "★".repeat(Math.floor(rate)) + "☆".repeat(5 - Math.floor(rate));
      return stars;
    },
  },
  methods: {
    removeAll() {
      this.products = [];
    },
    closeform() {
      this.stt = false;
    },
    dong() {
      this.rate = false;
    },

    xoa(id) {
      this.products = this.products.filter((item) => item.id !== id);
    },
    FilterL(list) {
      // Thay đổi trạng thái filter khi người dùng click vào nút tương ứng
      this.list = list;
    },
    addProduct(newProduct) {
      // Thêm sản phẩm mới vào danh sách
      this.products.push(newProduct);
      console.log(this.products);
    },
  },
};
</script>
<style>
#app {
  font-family: Arial;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

* {
  background-color: #ffff;
  max-width: 850px;
}

.header {
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
}

.saibar div button {
  border: none;
  font-weight: 900;
  font-family: inherit;
}

.saibar {
  display: flex;
  justify-content: space-between;
}

.tab {
  border-top: 1px solid #11cdef;
  margin-top: 10px;
}
</style>
