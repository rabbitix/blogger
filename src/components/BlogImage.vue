<template>
  <img :src="imageSrc" alt="photo" class="">


</template>
<script>
import axios from 'axios';

export default {
  name: 'BlogImage',

  props: ['url'],
  created() {
    //get img by url
    axios.get(this.url)
        .then(response => {
          this.imageSrc = response.data.media_details.sizes.medium_large.source_url
        })
  },
  data() {
    return {
      imageSrc: ''
    }
  },
}
</script>