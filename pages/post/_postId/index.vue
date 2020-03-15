// AUTO GENERATED FILE BY TETAMBA

<template>
  <v-row dense>
    <v-col v-for=" item in items" :key="item.title" :cols="item.flex">
        
      <v-card class="mx-auto" max-width="344">
        <v-img
          :src="item.src"
          class="white--text align-end"
          gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
          height="200px"
        ></v-img>

        <v-card-title>{{ item.title}}</v-card-title>

        <v-card-subtitle>{{item.content}}</v-card-subtitle>

        <v-card-actions>
          <v-btn :to="'/post/' + id + '/edit'">EDIT</v-btn>

          <v-spacer></v-spacer>

          <v-btn icon @click="show = !show">
            <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
          </v-btn>
        </v-card-actions>

        <v-expand-transition>
          <div v-show="show">
            <v-divider></v-divider>

            <v-card-text v-text="item.content"></v-card-text>
          </div>
        </v-expand-transition>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      props: ['id', 'userId', 'title', 'body'],
      item: {},
      id: this.$route.params.id
    }
  },
  mounted() {
    this.$axios
      .get('http://localhost:3001/posts/' + this.$route.params.id)
      .then((res) => {
        this.item = res.data || {}
      })
  }
}
</script>

<style></style>
