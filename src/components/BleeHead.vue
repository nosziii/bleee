<template>
  <v-container class="fill-height">
    <v-responsive class="d-flex align-center text-center fill-height">
      <v-img
        contain
        height="150"
        src="src/assets/logo.jpeg"
      />

      <div class="text-body-4 font-weight-light text-h4 mb-n1 head-title">Welcome to</div>

      <h1 class="text-h2 font-weight-bold head-title">Bleee</h1>

      <div class="py-5" />
      <v-card
        class="mx-auto"
        color="grey-lighten-3"
        max-width="400"
      >
        <v-card-text>
          <v-text-field
            :loading="loading"
            density="compact"
            variant="solo"
            label="Search sound"
            append-inner-icon="mdi-magnify"
            v-model="searchText"
            single-line
            hide-details
            @click:append-inner="onClick"
          ></v-text-field>
        </v-card-text>
      </v-card>
      <div class="py-5" />

      <v-row class="d-flex align-center justify-center">
        <v-col cols="auto" v-for="(card, index) in searchTitle" :key="index">
          <Card :card="card" :componentKey="index"/>
        </v-col>
      </v-row>
    </v-responsive>
  </v-container>
</template>

<script>
  import Card from './Card.vue'

export default {
    // created() {
    //   const storage = window.localStorage.getItem('bleeeSoundFavorit')
    //   if(!storage){
    //     window.localStorage.setItem('bleeeSoundFavorit', {})
    //   }
    // },
  data: () => ({
      searchText:'',
      loaded: false,
      loading: false,
      searchValue: [],
      soundAndPath:[
        {'title': 'Cancan', 'path': 'cancan15542.mp3'},
        {'title': 'Alarm', 'path': 'alarm.wav'},
        {'title': 'Dog', 'path': 'dogbarking.wav'},
        {'title': 'Cancan', 'path': 'cancan15542.mp3'},
        {'title': 'Birds Singing', 'path': 'birdssinging.wav'},
        {'title': 'Cartoon Failure Piano', 'path': 'cartoon-failure-piano.wav'},
        {'title': 'Cartoon Friendly Kiss', 'path': 'cartoon-friendly-kiss.wav'},
        {'title': 'Cartoon Sad Party Horn', 'path': 'cartoon-sad-party-horn.wav'},
        {'title': 'cartoon-voice-laugh', 'path': 'cartoon-voice-laugh.wav'},
        {'title': 'clock-countdown-bleeps', 'path': 'clock-countdown-bleeps.wav'},
        {'title': 'crowd-laugh', 'path': 'crowd-laugh.wav'},
        {'title': 'Crowd laugh', 'path': 'crowdlaugh.wav'},
        {'title': 'dog barking', 'path': 'dogbarking.wav'},
        {'title': 'drum-joke-accent', 'path': 'drum-joke-accent.wav'},
        {'title': 'epic-orchestra-transition', 'path': 'epic-orchestra-transition.wav'},
        {'title': 'female-astonished', 'path': 'female-astonished.wav'},
        {'title': 'intro-transition', 'path': 'intro-transition.wav'},
        {'title': 'joke-drums', 'path': 'joke-drums.wav'},
        {'title': 'laughing-cartoon-creature', 'path': 'laughing-cartoon-creature.wav'},
        {'title': 'Sad Game Over', 'path': 'sadgameover.wav'},
        {'title': 'sick-man-sneeze', 'path': 'sick-man-sneeze.wav'},
        {'title': 'Stadium Crowd', 'path': 'stadiumcrowd.wav'},
        {'title': 'Swoosh Heartbeat', 'path': 'swooshheartbeat.wav'},
        {'title': 'telephone-ringtone', 'path': 'telephone-ringtone.wav'},
        {'title': 'cseled', 'path': 'cseled.mp4'},
      ]
    }),
  computed:{
    searchTitle(){
      let term = this.searchText.toLowerCase()
      this.searchValue = this.soundAndPath.filter(item => item.title.toLowerCase().indexOf(term) > -1)
      return this.searchValue
    },
  },
  methods:{

    onClick () {
      this.loading = true
      setTimeout(() => {
        this.loading = false
        this.loaded = true
      }, 2000)
    },
  },
  components:{
    Card
  }
}

</script>

<style scoped>
.head-title {
  font-family: 'Ms Madi', cursive !important;
}
</style>
