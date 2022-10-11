<template>
  <div>
    <h1>รายละเอียดวันหยุด</h1>
    <p>วันที่-เดือน: {{ blog.title }}</p>
    <p>รายละเอียดวันหยุด: {{ blog.content }}</p>
    <p>สถานะ: {{ blog.status }}</p>
    <p>
      <button
        class="btn btn-primary "
        v-on:click="navigateTo('/blog/edit/' + blog.id)"
      >
        แก้ไขวันหยุด
      </button>
      <button class="btn btn-gray " v-on:click="navigateTo('/blogs')">
        ย้อนกลับ
      </button>
    </p>
  </div>
</template>
<script>
import BlogsService from "@/services/BlogsService";
export default {
  data() {
    return {
      blog: null
    };
  },
  async created() {
    try {
      let blogId = this.$route.params.blogId;
      this.blog = (await BlogsService.show(blogId)).data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    }
  }
};
</script>
<style scoped>
.btn-primary {
  color: white;
  background-color: green;
  text: bold;
  border-radius: 4;
}
.btn-gray {
  color: white;
  background-color: gray;
  text: bold;
  border-radius: 4;
}
</style>
