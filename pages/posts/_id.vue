<template>
  <div>
    <div v-for="data, index in imageDataList" :key="index">
      <div>id: {{ data.id }}</div>
      <div>tags: {{ data.tags }}</div>
      <img :src="data.webformatURL" :alt="data.id">
    </div>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: this.imageTags
    }
  },
  async asyncData({ $axios, params }) {
    const url = `https://pixabay.com/api?key=${process.env.api_key}&id=${params.id}`
    const data = await $axios.$get(url)
    const imageDataList = data.hits
    const imageTags = data.hits[0].tags

    return { imageDataList, imageTags }
  }
}
</script>
