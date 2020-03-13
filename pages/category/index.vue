<template>
  <v-data-table
    :headers="headers"
    :items="items"
    sort-by="id"
    class="elevation-1"
    @refresh-dong="fetchData"
  >
    <template v-slot:top>
      <v-toolbar flat color="black">
        <v-toolbar-title>Category</v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-spacer></v-spacer>
        <v-btn to="/category/create">
          <v-icon small class="mr-2">mdi-add</v-icon>Add
        </v-btn>
      </v-toolbar>
    </template>
    <template v-slot:item.actions="{ item }">
      <v-icon small class="mr-2" @click="editItem(item)">mdi-pencil</v-icon>
      <v-icon small @click="hapus(item)">mdi-delete</v-icon>
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
  computed: {},
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
  },
  hapus() {
    const setuju = confirm('are u sure?')
    if (!setuju) {
      return
    }

    this.$axios
      .delete('http://localhost:3001/category/' + this.id)
      .then((_) => {
        this.$router.push('/category')
      })
  }
}
</script>