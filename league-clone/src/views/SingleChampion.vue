<template>
  <main>
    <div class="stats-container">
      <div class="champion-name-container">
        <h1 class="champion-name">{{ this.name }}</h1>
      </div>
      <div class="champion-stats-container">
        <div class = "champion-stats">
          <span class = "stats">HP: {{ this.champion.hp }}</span> &nbsp; 
          <span class = "stats">MANA: {{ this.champion.mp }}</span>  &nbsp; 
          <span class = "stats">ARMOR: {{ this.champion.armor }}</span> &nbsp; 
          <span class = "stats">MAGIC RESISTANCE: {{ this.champion.spellblock }}</span> &nbsp;
          <span class = "stats">ATTACK DAMAGE: {{ this.champion.attackdamage }}</span>  &nbsp; 
          <span class = "stats">ATTACK RANGE: {{ this.champion.attackrange }}</span>   
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      champion: [],
      name: ''
    }
  },
  methods: {
    getChampion() {
      const options = {
        method: 'GET',
        url: `https://api.pandascore.co/lol/champions/${this.$route.params.id}`,
        headers: {
          accept: 'application/json',
          authorization: 'Bearer IhXJCEyOkxSbP1pdpvNSnS4feNb3VTiG1po9gNFMf0ByQvt6VkI'
        }
      }
      axios
        .request(options)
        .then((response) => {
          this.champion = response.data
          this.name = this.champion.name.toUpperCase()
          let nameHolder = response.data.name.replace(/'/g, '')

          let imageName = nameHolder + '_0'
          let imageLink = `https://ddragon.leagueoflegends.com/cdn/img/champion/splash/${imageName}.jpg`

          let media = window.matchMedia("(max-width: 500px)");
          const imageBody = document.querySelector('.champion-name-container');
          imageBody.style.backgroundImage = `url('${imageLink}')`


        })
        .catch((error) => {
          console.error(error)
        })
    },
  },
  mounted() {
    this.getChampion()
  }
}
</script>
