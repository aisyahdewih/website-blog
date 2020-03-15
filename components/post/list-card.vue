<template>
  <v-container>
    <v-card-title>{{title}}</v-card-title>

    <v-card-subtitle>{{content}}</v-card-subtitle>

    <v-card-actions>
      <v-btn text>View</v-btn>
      <v-btn text>Edit</v-btn>
      <v-btn color="purple" text>Delete</v-btn>
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
  methods: {
    hapus() {
      const setuju = confirm('anda yakin?')
      if (!setuju) {
        return
      }

      this.$axios.delete('http://localhost:3000/posts/' + this.id).then((_) => {
        this.$emit('refresh-dong')
      })
    }
  }
}
</script>