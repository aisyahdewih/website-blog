<template>
  <v-data-table
    :headers="headers"
    :items="items"
    :search="search"
    sort-by="id"
    sort-field="field"
    sort-desc="true"
    class="elevation-1"
    @refresh-dong="fetchData"
  >
    <template v-slot:top>
      <v-toolbar flat color="red lighten-4">
        <v-toolbar-title>Category</v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          single-line
          hide-details
        ></v-text-field>
        <v-spacer></v-spacer>
        <v-btn to="/category/create"   color="red lighten-3">
          <v-icon small class="mr-2">mdi-add</v-icon>Add
        </v-btn>
      </v-toolbar>
    </template>
    <template v-slot:item.actions="{ item }">
      <nuxt-link :to="'/category/' + item.id">
        <v-icon small class="mr-2" color="pink">mdi-eye</v-icon>
      </nuxt-link>
      <nuxt-link :to=" '/category/' + item.id + '/edit'">
        <v-icon small class="mr-2" color="pink">mdi-pencil</v-icon>
      </nuxt-link>
      <v-icon small @click="hapus(item.id)" color="pink">mdi-delete</v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn color="primary" @click="fetchData">Reset</v-btn>
    </template>
  </v-data-table>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      id: this.$route.params.catId,
      search: '',
      dialog: false,
      headers: [
        {
          text: 'ID',
          align: 'start',
          sortable: false,
          value: 'id'
        },
        { text: 'TITLE', value: 'title' },
        { text: 'Actions', value: 'actions', sortable: false }
      ],
      items: [],

      defaultItem: {
        title: ''
      }
    }
  },
  mounted() {
    this.fetchData()
  },
  computed: {},
  methods: {
    async fetchData() {
      const res = await this.$axios.get(`http://localhost:3000/category`)
      this.items = res.data
    },
    hapus(id) {
      const setuju = confirm('are u sure?')
      if (!setuju) {
        return
      }
      this.$axios.delete('http://localhost:3000/category/' + id).then((_) => {
        this.fetchData()
      })
    }
  },
  watch: {
    dialog(val) {
      val || this.close()
    }
  }
}
</script>