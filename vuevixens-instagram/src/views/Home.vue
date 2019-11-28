<template>
    <div>
    <the-header
      :step="step"
      @go-to-home="handleGoToHome"
      @next-step="step++"
      @share-post="handleSharePost"/>
    <the-container
      :step="step"
      :posts="posts"
      :filters="filters"
      :image="image"
      v-model="caption"
      @filter-selected="handleFilterSelected"/>
      <the-footer
    :step="step"
    @go-to-home="handleGoToHome"
    @upload-image="handleUploadImage"/>
  </div>
</template>

<script>
import TheHeader from '@/components/TheHeader.vue'
import TheContainer from '@/components/TheContainer.vue'
import TheFooter from '@/components/TheFooter.vue'
import posts from '@/data/posts'
import filters from '@/data/filters'

export default {
  name: 'Home',
  data () {
    return {
      posts,
      filters,
      caption: '',
      image: '',
      step: 1
    }
  },
  components: {
    TheHeader,
    TheContainer,
    TheFooter
  },
  methods: {
    handleGoToHome () {
      this.step = 1
    },
    handleSharePost () {
      this.handleGoToHome()
    },
    handleUploadImage (ev) {
      const files = ev.target.files
      if (!files.length) return

      const reader = new FileReader()
      reader.readAsDataURL(files[0])
      reader.onload = ev => {
        this.image = ev.target.result
        this.step = 2
      }
      document.querySelector('#file').value = ''
    }
  }
}
</script>
