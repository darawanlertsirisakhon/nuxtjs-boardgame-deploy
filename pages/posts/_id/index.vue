<template>
  <div>
    <SinglePost :post="singlePost" />
  </div>
</template>
<script>
import SinglePost from '../../../components/posts/SinglePost.vue'
import axios from 'axios'
export default {
  layout: 'coreLayout',
  components: {
    SinglePost,
  },
  asyncData(context) {
    return axios
      .get(
        'https://boardgame-nuxtjs-default-rtdb.asia-southeast1.firebasedatabase.app/post/' +
          context.params.id +
          '.json'
      )
      .then((res) => {
        return {
          singlePost: {
            ...res.data,
            id: context.params.id,
          },
        }
      })
      .catch((e) => context.error(e))
  },
}
</script>
