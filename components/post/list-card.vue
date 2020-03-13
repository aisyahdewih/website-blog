<template>
  <v-card class="mx-auto" max-width="344">
    <v-img
      :src="item.src"
      class="white--text align-end"
      gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
      height="200px"
    ></v-img>

    <v-card-title>{{title}}</v-card-title>

    <v-card-subtitle>{{content}}</v-card-subtitle>

    <v-card-actions>
      <v-btn :to="'/post/' + id + '/edit'">EDIT</v-btn>
      <v-btn color="purple" text>DELETE</v-btn>

      <v-spacer></v-spacer>

      <v-btn icon @click="show = !show">
        <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>{{ content }}</v-card-text>
      </div>
    </v-expand-transition>
  </v-card>
</template>
<script>
export default {
  props: ['title', 'content']
}
</script>
