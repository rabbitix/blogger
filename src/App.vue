<template >
  <div id="wrapper" class="dark">
    <blog-posts v-for="link in links" :tit="link.title" :href="link.address" :key="link.title"></blog-posts>
    <!-- <blog-posts :href="'https://blog.exsib.com'" ></blog-posts> -->
  </div>
</template>

<script>
import BlogPosts from "./components/BlogPosts";
import axios from 'axios';

export default {
  name: "App",
  components: {
    BlogPosts,
  },
  created(){
    axios.get(this.url)
        .then(response => {
          console.log(response);
          this.links = response.data;
        })
  },
  data() {
    return {
      links: [],
      url:"https://0sa2vx.deta.dev/blogs"
    };
  },
};
</script>

