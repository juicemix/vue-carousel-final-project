<template lang="pug">
  #app
    //img(alt="Vue logo" src="./assets/logo.png")
    //Carousel(:slides="images" ipv="1")
    //HelloWorld(msg="Welcome to Your Vue.js App")
    Carousel(:images="images" startingImage="0" showProgressBar=true )
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Carousel from './components/Carousel'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Carousel
  },
  data: function() {
    return {
      images: [
          {
              id: 1,
              big: 'https://vignette.wikia.nocookie.net/marveldatabase/images/e/e7/Iron_Man_Vol_4_6_Textless.jpg/revision/latest?cb=20100309183023',
              thumb: 'https://vignette.wikia.nocookie.net/marveldatabase/images/e/e7/Iron_Man_Vol_4_6_Textless.jpg/revision/latest?cb=20100309183023'
          },
          {
              id: 2,
              big: 'https://vignette.wikia.nocookie.net/marveldatabase/images/9/96/Friendly_Neighborhood_Spider-Man_Vol_2_8_Granov_Variant_Textless.jpg/revision/latest?cb=20190608001208',
              thumb: 'https://vignette.wikia.nocookie.net/marveldatabase/images/9/96/Friendly_Neighborhood_Spider-Man_Vol_2_8_Granov_Variant_Textless.jpg/revision/latest?cb=20190608001208'
          },
          {
              id: 3,
              big: 'https://vignette.wikia.nocookie.net/marveldatabase/images/2/2b/Return_of_Wolverine_Vol_1_2_Dell%27Otto_Variant_Textless.jpg/revision/latest?cb=20190320201036',
              thumb: 'https://vignette.wikia.nocookie.net/marveldatabase/images/2/2b/Return_of_Wolverine_Vol_1_2_Dell%27Otto_Variant_Textless.jpg/revision/latest?cb=20190320201036'
          },
          {
              id: 4,
              big: 'https://vignette.wikia.nocookie.net/marveldatabase/images/d/dc/Immortal_Hulk_20_Unknown_Comic_Books_Exclusive_Virgin_Variant.jpg/revision/latest?cb=20190830071143',
              thumb: 'https://vignette.wikia.nocookie.net/marveldatabase/images/d/dc/Immortal_Hulk_20_Unknown_Comic_Books_Exclusive_Virgin_Variant.jpg/revision/latest?cb=20190830071143'
          },
          {
              id: 5,
              big: 'https://vignette.wikia.nocookie.net/marveldatabase/images/e/e1/Max_Eisenhardt_%28Earth-616%29_from_House_of_X_Vol_1_1_001_%281%29.png/revision/latest?cb=20190724212749',
              thumb: 'https://vignette.wikia.nocookie.net/marveldatabase/images/e/e1/Max_Eisenhardt_%28Earth-616%29_from_House_of_X_Vol_1_1_001_%281%29.png/revision/latest?cb=20190724212749'
          }
      ]
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
