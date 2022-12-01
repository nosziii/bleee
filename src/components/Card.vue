<template>
  <v-card
    class="mx-auto"
    max-width="200"
    min-width="200"
  >
    <v-img
      class="align-end text-white"
      height="100"
      src="src/assets/soundwave.webp"
      cover
    >
    </v-img>

    <v-card-subtitle class="pt-4 sound-title">
      {{nameParsed(card.title)}}
    </v-card-subtitle>

    <v-card-actions>
      <v-img
      v-if="!disabled"
      class="align-end text-white"
      height="100"
      width="100"
      src="src/assets/playButton.png"
      @click="audioPlay(card.path)"
    >
      </v-img>
      <v-img
      v-if="disabled"
      class="align-end text-white"
      height="100"
      width="100"
      src="src/assets/stopButton.png"
      @click="audioStop()"
    >
      </v-img>
    </v-card-actions>
      <v-icon
        title="Add the favorit"
        size="large"
        color="yellow-darken-2"
        @click="favorit"
      >
        mdi-star-outline
      </v-icon>
  </v-card>
</template>

<script>
  export default {
    name: 'Card',
    props: ['card', 'componentKey'],
    data: () => {
      return {
        audio: '',
        buttonStyle: false
      }
    },
    methods:{
      audioPlay(sound){
        this.buttonStyle = true
        this.audio = new Audio(`src/assets/sound/${sound}`)
        this.audio.play()
        this.audio.onended = function() {
          this.audioStop()
        }.bind(this)
      },
      audioStop(){
        this.buttonStyle = false
        this.audio.pause()
      },
      nameParsed(name){
        const parsedName = name.replaceAll('-', ' ').toLowerCase()
        return parsedName
      },
      favorit(){
        const storage = window.localStorage.getItem('bleeeSoundFavorit')
        let store = []
        if (storage && JSON.parse(storage) && JSON.parse(storage).length){
          const jsonStore = JSON.parse(storage)
          store = jsonStore.filter(st => st.title.toLowerCase()  === this.card.title.toLowerCase())
          if(store && store.length) {

          }
          console.log("==== store jepepepepp", store)
        }else{
          let cardArray = []
          cardArray.push({'title': this.card.title.toLowerCase()})
          console.log("==== cardArray", cardArray)
          window.localStorage.setItem('bleeeSoundFavorit', JSON.stringify(cardArray))
        }
        // this.componentKey

      },
      deleteStore(param){

      },
    },
    computed:{
      disabled(){
        return this.buttonStyle
      }
    },
    components:{
    }
}
</script>

<style scoped>
.sound-title {
  font-family: 'Caveat', cursive;
  font-weight: 800;
  font-size: 1.2rem;
}
.actived {
  background-color: lightgreen;
}
</style>
