<template>
  <div>
    <div class="nv-navbar">
      <ul class="nav">
        <li><router-link :to="{ name: 'app' }">หน้าหลัก</router-link></li>
        <li><router-link :to="{ name: 'blogs' }">ตารางวันหยุด</router-link></li>
      </ul>
      <div class="clearfix" />
    </div>
  </div>
</template>
<script>
export default {};
</script>
<style scoped>
.nv-navbar {
  background-color: palegoldenrod;
  width: 100%;
  padding: 10px 0px 10px 0px;
}
.nv-navbar .nav {
  list-style: none;
  margin: 0;
  padding: 0;
  float: left;
}
.nv-navbar .nav li {
  float: left;
}
.nv-navbar .nav li a {
  padding: 10px;
  text-decoration: none;
  color: grey;
  font-weight: bold;
}
.nv-navbar .nav li a:hover {
  padding: 10px;
  text-decoration: none;
  color: darkslategrey;
}
.nv-navbar .nav li a.router-link-active {
  background-color: gold;
  color: darkslategrey;
}
.clearfix {
  clear: left;
}
</style>
