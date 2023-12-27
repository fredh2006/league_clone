<script setup></script>

<template>
  <main>
    <div class="hero-text">
      <div id="hero-title">CHOOSE YOUR <span id="champion"></span></div>
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
    rotateWords() {
    const dynamicText = document.getElementById("champion")
    const words = ['MAGE', 'TANK', 'FIGHTER', 'SUPPORT', 'ASSASSIN', 'MARKSMEN', 'CHAMPION']
    // Variables to track the position and deletion status of the word
    let wordIndex = 0
    let charIndex = 0
    let isDeleting = false
    let timesRun = 0;
    const typeEffect = () => {
      const currentWord = words[wordIndex]
      const currentChar = currentWord.substring(0, charIndex)
      dynamicText.textContent = currentChar
      dynamicText.classList.add('stop-blinking')
      
      if(timesRun<13){

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
        timesRun++;
      }

    }

    }
      typeEffect();
  },
  },
  mounted() {
    // this.fetchChampions()
    this.rotateWords();
  }
}
</script>
