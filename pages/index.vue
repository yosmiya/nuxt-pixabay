<template>
  <div>
    <div>
      <select v-model="apiTarget">
        <option v-for="option, index in apiTargetList" :key="index" :value="option.title">{{ option.title }}</option>
      </select>
      <button @click="getImageDataList">検索</button>
      <div v-if="dataListLength">
        <h1>検索結果</h1>
        <ul class="dataList">
          <li v-for="data, index in imageDataList" :key="index">
            <nuxt-link :to="`/posts/${data.id}`">
              <img :src="data.previewURL" :alt="data.id">
            </nuxt-link>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // middleware: 'consoleLog',
  data() {
    return {
      imageDataList: [],
      dataListLength: 0,
      apiTargetList: [
        { title: 'red', id: 'red' },
        { title: 'green', id: 'green' },
        { title: 'blue', id: 'blue' },
      ],
      apiTarget: 'red',
    }
  },
  head() {
    return {
      title: 'TOP PAGE',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'My custom description'
        }
      ]
    }
  },
  methods: {
    async getImageDataList() {
      const url = `https://pixabay.com/api?key=${process.env.api_key}&image_type=photo&q=${this.apiTarget}`
      const data = await this.$axios.$get(url)
      this.imageDataList = data.hits
      this.dataListLength = data.hits.length
    }
  },
}
</script>

<style lang="scss" scoped>
.dataList {
  display: flex;
  flex-wrap: wrap;

  li {
    list-style-type: none;
  }
}
</style>