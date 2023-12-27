<script setup></script>

<template>
  <main>
    <div class="hero-text">
      <div id="hero-title">CHOOSE YOUR</div>
      <div id="champion">CHAMPION
      </div>
    </div>
    <div id="hero-description">
      <p>
        With more than 140 champions, you'll find the perfect match for your playstyle. Master one,
        or master them all.
      </p>
    </div>
  </main>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      words: []
    }
  },
  methods: {
    // fetchChampions() {
    //   const options = {
    //     method: 'GET',
    //     url: 'https://api.pandascore.co/lol/champions',
    //     params: { sort: '', page: '1', per_page: '100' },
    //     headers: {
    //       accept: 'application/json',
    //       authorization: 'Bearer IhXJCEyOkxSbP1pdpvNSnS4feNb3VTiG1po9gNFMf0ByQvt6VkI'
    //     }
    //   }
    //   axios
    //     .request(options)
    //     .then(function (response) {
    //       console.log(response.data)
    //     })
    //     .catch(function (error) {
    //       console.error(error)
    //     })
    // }
  },
  mounted() {
    // this.fetchChampions()
  }
}
</script>
