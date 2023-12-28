<script setup></script>

<template>
  <main>
    <div class="hero">
      <div class="hero-text">
        <div id="hero-title">CHOOSE YOUR</div>
        <div id="champion"></div>
      </div>
      <div id="hero-description">
        <p>
          With more than 140 champions, you'll find the perfect match for your playstyle. Master
          one, or master them all.
        </p>
      </div>
    </div>

    <div class="champion-container columns">
      <div class="column is-one-fifth" id="columnOne"></div>
      <div class="column is-one-fifth" id="columnTwo"></div>
      <div class="column is-one-fifth" id="columnThree"></div>
      <div class="column is-one-fifth" id="columnFour"></div>
      <div class="column is-one-fifth" id="columnFive"></div>
    </div>
  </main>
</template>

<script>
import axios, { formToJSON } from 'axios'

export default {
  data() {
    return {
      words: [],
      champions: [],
      columns: []
    }
  },
  methods: {
    fetchChampions() {
      for (let i = 1; i <= 2; i++) {
        const options = {
          method: 'GET',
          url: 'https://api.pandascore.co/lol/champions',
          params: { sort: 'name', page: `${i}`, per_page: '100' },
          headers: {
            accept: 'application/json',
            authorization: 'Bearer IhXJCEyOkxSbP1pdpvNSnS4feNb3VTiG1po9gNFMf0ByQvt6VkI'
          }
        }
        axios
          .request(options)
          .then((response) => {
            let champions = response.data
            this.champions = champions
            this.generateChampionCards(this.champions)
          })
          .catch((error) => {
            console.error(error)
          })
      }
    },
    typeWords() {
      const dynamicText = document.getElementById('champion')
      const words = ['MAGE', 'TANK', 'FIGHTER', 'SUPPORT', 'ASSASSIN', 'MARKSMEN', 'CHAMPION']
      // Variables to track the position and deletion status of the word
      let wordIndex = 0
      let charIndex = 0
      let isDeleting = false
      let timesRun = 0
      const typeEffect = () => {
        const currentWord = words[wordIndex]
        const currentChar = currentWord.substring(0, charIndex)
        dynamicText.textContent = currentChar
        dynamicText.classList.add('stop-blinking')

        if (timesRun < 13) {
          if (!isDeleting && charIndex < currentWord.length) {
            // If condition is true, type the next character
            charIndex++
            setTimeout(typeEffect, 200)
          } else if (isDeleting && charIndex > 0) {
            // If condition is true, remove the previous character
            charIndex--
            setTimeout(typeEffect, 200)
          } else {
            // If word is deleted then switch to the next word
            isDeleting = !isDeleting
            dynamicText.classList.remove('stop-blinking')
            wordIndex = !isDeleting ? (wordIndex + 1) % words.length : wordIndex
            setTimeout(typeEffect, 10)
            timesRun++
          }
        }
      }
      typeEffect()
    },
    generateChampionCards(champions) {
      let column = document.querySelectorAll('.column');
      this.columns = column


      let currColumn = 0
      for (let i = 0; i < champions.length; i++) {
        if (currColumn % 5 == 0) {
          currColumn = 0
        }
        let card = document.createElement('div')
        card.classList.add('card')

        let img = new Image()
        img.src = champions[i].big_image_url
        img.classList.add('card-image')

        let name = document.createElement('span')
        let pContainer = document.createElement('span')
        pContainer.classList.add('name')
        let p = document.createElement('p')
        let titleContent = document.createTextNode(champions[i].name.toUpperCase())
        p.appendChild(titleContent)
        pContainer.appendChild(p)
        name.appendChild(pContainer)
        name.classList.add('name-container')

        card.appendChild(img)
        card.appendChild(name)

        this.columns[currColumn].appendChild(card)
        currColumn++
      }
    }
  },
  mounted() {
    this.fetchChampions()
    this.typeWords()
  }
}
</script>
