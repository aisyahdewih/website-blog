<template>
  <v-card
    max-width="344"
  ><br>
    <v-img
      src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
      height="200px"
    ></v-img>

    <v-card-title>
      Top western road trips
    </v-card-title>

    <v-card-subtitle>
      1,000 miles of wonder
    </v-card-subtitle>

    <template v-slot:button>
              <nuxt-link :to="`/books/${item.title}`">
                <v-btn>View</v-btn>
              </nuxt-link>
              <v-btn @click.stop="edit(item,index)">Edit</v-btn>
              <v-btn @click.stop="remove(item.category, index)">Remove</v-btn>
  </template>
  </v-card>
</template>
<script>
  export default {
    data: () => ({
      show: false,
    }),
  }
</script>