<template>
  <v-carousel
    cycle
    height="400"
    hide-delimiter-background
    show-arrows-on-hover
  >
    <v-carousel-item
      v-for="(slide, i) in slides"
      :key="i"
    >
      <v-sheet
        :image="images[i]"
        height="100%"
      >
        <v-row
          class="fill-height"
          align="center"
          justify="center"
        >
          <div class="display-3">{{ slide }} Slide</div>
        </v-row>
      </v-sheet>
    </v-carousel-item>
  </v-carousel>
</template>
<script>
  export default {
    data () {
      return {
        images: [
          'https://www.google.com/url?sa=i&url=https%3A%2F%2Fmakassar.terkini.id%2Fakibat-perubahan-iklim-4-pohon-ini-terancam-punah-dari-muka-bumi%2F&psig=AOvVaw2WNu2KQV-oG5ArSMuqW5Ri&ust=1584166330788000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCOj9itLllugCFQAAAAAdAAAAABAD',
          'warning',
          'pink darken-2',
          'red lighten-1',
          'deep-purple accent-4',
        ],
        slides: [
          'First',
          'Second',
          'Third',
          'Fourth',
          'Fifth',
        ],
      }
    },
  }
</script>