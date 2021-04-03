<template>

  <div class="p-5 dark:bg-gray-800">
    <div class="">
      <h2
          class=" sm:text-right
           border p-1.5 w-max dark:text-gray-50
          font-semibold font-serif mb-2 transform -skew-x-6 hover:skew-x-0"
      >Latest <span class=" dark:text-green-500">{{this.tit}}  Blog posts</span>
      </h2>

      <div class="blog-posts grid gap-6 grid-cols-1 sm:grid-cols-2 md:grid-cols-3">
        <div v-for="post in posts" :key="post.id" class="flex flex-col">
          <div id="post" class="border rounded border-2
          bg-gray-100 dark:bg-gray-700
          border-green-900 shadow-2xl p-1">
            <blog-image class="rounded p-1 object-cover"
                        :url="post._links['wp:featuredmedia'][0].href">
            </blog-image>
            <div class="p-3">
              <a :href="post.link">
                <h2 class="text-right font-semibold dark:text-gray-300 mb-2 ">{{
                    post.title.rendered
                  }}</h2></a>
              <!--              <div class="post_meta">-->
              <!--                <span>31 خرداد 1399</span>-->
              <!--                <span><i class="fa fa-comment-o"></i> 4</span>-->
              <!--                <span><i class="fa fa-eye"></i> 50</span>-->
              <!--              </div>-->
              <div class="text-right text-justify dark:text-gray-200">
                {{ stripTags(post.excerpt.rendered) }}
              </div>


              <div id="more" class="text-right mt-4">
                <a :href="post.link" class="flex flex-row-reverse justify-between">
                  <span class="">مشاهده‌ی بیشتر</span>
                  <i class=" fa fa-arrow-left"></i>
                </a>
              </div>
            </div>
          </div>

        </div>
      </div>
    </div> <!-- end container -->
  </div> <!-- end blog-section -->
</template>

<script>
import BlogImage from './BlogImage'
import sanitizeHtml from 'sanitize-html'
import axios from 'axios';

export default {
  components: {
    BlogImage,
  },
  created() {
    console.log(this.href)
    axios.get(this.href + '/wp-json/wp/v2/posts?per_page=3')
        .then(response => {
          this.posts = response.data
        })
  },
  props: [
    'href','tit'
  ],
  data() {
    return {
      posts: []
    }
  },
  methods: {
    stripTags(html) {
      return sanitizeHtml(html, {
        allowedTags: []
      }).substring(0, 150)
    }
  }

}

</script>

<!--<style>-->

<!--.blog-section {-->
<!--  background: #f0f0f0;-->
<!--  border-top: 1px solid #CDCDCD;-->
<!--  border-bottom: 1px solid #00000011;-->
<!--  padding: 50px 0;-->
<!--  grid-area: blog-section;-->
<!--}-->

<!--.blog-section .somePost {-->
<!--  text-align: center;-->
<!--  font-size: 19px;-->
<!--  color: #003a48;-->
<!--  margin-bottom: 38px;-->
<!--}-->

<!--.blog-section .somePost span {-->
<!--  color: #960000;-->
<!--}-->

<!--.blog-section .blog-posts {-->
<!--  display: grid;-->
<!--  grid-template-columns: 1fr 1fr 1fr;-->
<!--  grid-gap: 30px;-->
<!--  margin: 40px 0 20px;-->
<!--  grid-template-areas: "blog1 blog2 blog3";-->
<!--}-->

<!--.blog-section .blog-posts .blog-post {-->
<!--  display: flex;-->
<!--  flex-direction: column;-->
<!--  background: #fff;-->
<!--  border: 1px solid #00000011;-->
<!--  border-radius: 8px;-->
<!--  overflow: hidden;-->
<!--  padding: 0;-->
<!--  box-shadow: 0 0 5px #00000022;-->
<!--  transition: 0.6s;-->
<!--}-->

<!--.blog-section .blog-posts .blog-post .blogImage {-->
<!--  width: 100%;-->
<!--  height: 240px;-->
<!--  -o-object-fit: cover;-->
<!--  object-fit: cover;-->
<!--  border-radius: 6px;-->
<!--  margin-left: 16px;-->
<!--}-->

<!--.blog-section .blog-posts .blog-post .blogPostContain {-->
<!--  padding: 1.6em 1.8em;-->
<!--  padding-bottom: 1em;-->
<!--  flex: 1;-->
<!--}-->

<!--.blog-section .blog-posts .blog-post .blogPostContain .blog-title {-->
<!--  font-size: 19px;-->
<!--  font-weight: 400;-->
<!--}-->

<!--.blog-section .blog-posts .blog-post .blogPostContain .blog-description {-->
<!--  font-size: 14px;-->
<!--  color: #555;-->
<!--  text-align: justify;-->
<!--  padding-left: 10px;-->
<!--  padding-bottom: 10px;-->
<!--  flex: 1;-->
<!--}-->

<!--.blog-section .blog-posts .blog-post .blogPostContain .post_meta {-->
<!--  font-size: 13px;-->
<!--  color: #777;-->
<!--  margin: 5px 0 7px 0;-->
<!--}-->

<!--.blog-section .blog-posts .blog-post .blogPostContain .post_meta span {-->
<!--  margin-left: 10px;-->
<!--}-->

<!--.blog-section .blog-posts .blog-post .blogPostContain .post_meta span i {-->
<!--  font-size: 11px;-->
<!--}-->

<!--.blog-section .blog-posts .blog-post .moreBtn {-->
<!--  display: flex;-->
<!--  flex-direction: row;-->
<!--  justify-content: space-between;-->
<!--  font-size: 14px;-->
<!--  border-top: 1px solid #00000022;-->
<!--  margin: 0 -2.3em;-->
<!--  padding: 13px 2.3em 0 2.3em;-->
<!--  text-decoration: none !important;-->
<!--  color: #000;-->
<!--  font-weight: 400;-->
<!--}-->

<!--.blog-section .blog-posts #blog1 {-->
<!--  grid-area: blog1;-->
<!--}-->

<!--.blog-section .blog-posts #blog2 {-->
<!--  grid-area: blog2;-->
<!--}-->

<!--.blog-section .blog-posts #blog3 {-->
<!--  grid-area: blog3;-->
<!--}-->
<!--</style>-->