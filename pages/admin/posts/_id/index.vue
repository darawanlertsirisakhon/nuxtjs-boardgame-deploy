<template>
  <div>
    <AdminForm @sendData="onSubmitted" :post="singlePost" />
  </div>
</template>
<script>
import AdminForm from '../../../../components/admin/AdminForm.vue'
import axios from 'axios'
export default {
  layout: 'coreLayout',
  components: {
    AdminForm,
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
  methods: {
    onSubmitted(postData) {
      this.$store.dispatch('editPost', postData).then(() => {
        this.$router.push('/admin/posts')
      })
    },
  },
}
</script>
