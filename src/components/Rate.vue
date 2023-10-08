<template>
  chào
  <button @click="$emit('cancel')">Close</button>
</template>

<style>
.img-fluid {
  width: 50px;
  border-radius: 50px;
  height: 60px;
}
</style>

<script>
export default {
  emits: ["cancel"],
  data() {
    return {
      rating: "5", // Giá trị mặc định cho đánh giá sao
      comment: "", // Giá trị mặc định cho bình luận
    };
  },
  methods: {
    submitReview() {
      // Ở đây, bạn có thể gửi đánh giá và bình luận đi đâu đó hoặc xử lý theo nhu cầu của bạn
      console.log("Sao: " + this.rating);
      console.log("Bình Luận: " + this.comment);
    },
  },
};
</script>
