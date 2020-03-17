<template>
  <v-container>
    <v-img
      :src="src"
      class="white--text align-end"
      gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
      height="200px"
    ></v-img>
    <v-card-title>{{title}}</v-card-title>

    <v-card-subtitle>{{ content }}</v-card-subtitle>

    <v-card-actions>
      <v-btn :to=" '/post/' + id + '/edit'">
        <v-icon small class="mr-2" color="teal lighten-1">mdi-pencil</v-icon>Edit
      </v-btn>
      <v-btn @click="hapus">
        <v-icon small  color="teal lighten-1">mdi-delete</v-icon>Delete
      </v-btn>

      <v-spacer></v-spacer>

      <v-btn icon @click="show = !show">
        <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>
        <v-card-text>{{content}}</v-card-text>
      </div>
    </v-expand-transition>
  </v-container>
</template>
<script>
export default {
  props: ['id', 'title', 'content', 'src', 'category_id'],
  data() {
    return {
      show: false
    }
  },
  methods: {
    hapus() {
      const setuju = confirm('anda yakin?')
      if (!setuju) {
        return
      }

      this.$axios.delete('http://localhost:3000/posts/' + this.id).then((_) => {
        this.$emit('refresh-ya')
      })
    }
  }
}
</script>