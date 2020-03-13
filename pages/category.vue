<template>
  <v-data-table :headers="headers" :items="items" sort-by="title" class="elevation-1">
    <template v-slot:top>
      <v-toolbar flat color="black">
        <v-toolbar-title>CATEGORY</v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-spacer></v-spacer>
        <v-btn>Add Category</v-btn>
      </v-toolbar>
    </template>

    <template v-slot:no-data>
      <v-btn color="primary" @click="fetchData">Reset</v-btn>
    </template>
  </v-data-table>
</template>


</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      dialog: false,
      headers: [
        {
          text: 'ID',
          align: 'start',
          sortable: false,
          value: 'id'
        },
        { text: 'TITLE', value: 'title' }
      ],
      items: [],
      editedIndex: -1,
      editedItem: {
        title: ''
      },
      defaultItem: {
        title: ''
      }
    }
  },
  mounted() {
    this.fetchData()
  },
  computed: {
    // formTitle() {
    //   return this.editedIndex === -1 ? 'New Category' : 'Edit Category'
    // }
  },
  methods: {
    async fetchData() {
      const res = await this.$axios.get(`http://localhost:3000/category`)
      this.items = res.data
    }
  },
  watch: {
    dialog(val) {
      val || this.close()
    }
  }
}
</script>