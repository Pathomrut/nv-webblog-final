<template>
  <div>
    <!-- <h4>จํานวน blog {{ blogs.length }}</h4> -->
    <p>
      <button class="btn btn-gray " v-on:click="navigateTo('/blog/create')">
        สร้างวันหยุด
      </button>
    </p>
    <div v-for="blog in blogs" v-bind:key="blog.id">
      <p><b>วันที่-เดือน</b> {{ blog.title }}</p>
      <p><b>รายละเอียดวันหยุด:</b> {{ blog.content }}</p>
      <p><b>สถานะ:</b> {{ blog.status }}</p>
      <p>
        <button
          class="btn btn-primary "
          v-on:click="navigateTo('/blog/' + blog.id)"
        >
          ดูรายละเอียดวันหยุด
        </button>
        <button
          class="btn btn-gray "
          v-on:click="navigateTo('/blog/edit/' + blog.id)"
        >
          แก้ไขวันหยุด
        </button>
        <button class="btn btn-red " v-on:click="deleteBlog(blog)">
          ลบข้อมูลวันหยุด
        </button>
      </p>
      <hr />
    </div>
  </div>
</template>
<script>
import BlogsService from "@/services/BlogsService";
export default {
  data() {
    return {
      blogs: []
    };
  },
  async created() {
    this.blogs = (await BlogsService.index()).data;
  },
  methods: {
    logout() {
      this.$store.dispatch("setToken", null);
      this.$store.dispatch("setBlog", null);
      this.$router.push({
        name: "login"
      });
    },
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteBlog(blog) {
      let result = confirm("Want to delete?");
      if (result) {
        try {
          await BlogsService.delete(blog);
          this.refreshData();
        } catch (err) {
          console.log(err);
        }
      }
    },
    async refreshData() {
      this.blogs = (await BlogsService.index()).data;
    }
  }
};
</script>
<style scoped>
.btn-gray {
  color: white;
  background-color: gray;
  text: bold;
  border-radius: 4;
}

.btn-primary {
  color: white;
  background-color: green;
  text: bold;
  border-radius: 4;
}
.btn-red {
  color: white;
  background-color: red;
  text: bold;
  border-radius: 4;
}
</style>
