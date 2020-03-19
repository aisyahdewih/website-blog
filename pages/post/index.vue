<template>
  <v-container fluid>
    <v-row no-gutters>
      <v-col>
        <div class="pa-2" outlined tile>
          <v-btn color="red lighten-3" to="/post/create" flex="right">
            <v-icon small class="mr-2">mdi-add</v-icon>Add
          </v-btn>
        </div>
      </v-col>
      <v-col class="d-flex" cols="12" sm="3">
        <div class="pa-2" outlined tile>
          <v-select
            v-bind:items="categories"
            label="Category"
            v-model="categoryFilter"
            item-text="title"
            item-value="id"
          ></v-select>
         
          <v-btn small outlined color="primary" @click="filter">Filter</v-btn>
        </div>
      </v-col>
      <v-col class="d-flex" cols="12" sm="3">
        <div class="pa-2" outlined tile>
          <v-text-field v-model="query" label="Search" append-icon="mdi-magnify"></v-text-field>
          <v-btn small outlined color="primary" @click="cari">Search</v-btn>
        </div>
      </v-col>
    </v-row>
    <v-container>
      <v-row dense>
        <v-col
          v-for="item in items"
          :key="item.title"
          :cols="item.flex"
          v-bind:pagination.sync="pagination"
          hide-actions
          class="elevation-1"
        >
          <v-card class="mx-auto" max-width="344">
            <ListCard
              :id="item.id"
              :key="String(item.title)"
              :title="item.title"
              :category_id="item.category_id"
              :content="item.content"
              :src="item.src"
              :cols="item.flex"
              @refresh-ya="refresh"
            ></ListCard>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-container>
</template>

<script>
import ListCard from '~/components/post/list-card'
import Multiselect from 'vue-multiselect'

export default {
  components: { ListCard, Multiselect },
  data() {
    return {
      items: [],
      id: this.$route.params.id,
      query: '',
      isError: false,
      isEmpty: false,
      isLoading: false,
      pagination: { sortBy: 'id', descending: true, rowsPerPage: -1 },
      categories: [],
      categoryFilter: ''
    }
  },
  mounted() {
    this.refresh()
    this.getCategory()
  },
  watch: {
    categoryFilter() {
      this.filter()
    }
  },
  methods: {
    async cari() {
      this.isLoading = true
      try {
        const res = await this.$axios.get('http://localhost:3000/posts', {
          params: {
            q: this.query
          }
        })
        this.items = res.data
        if (this.items.length === 0) {
          this.isEmpty = true
        }
      } catch (err) {
        this.isError = true
      }
      this.isLoading = false
    },
    async filter() {
      const res = await this.$axios.get(
        `http://localhost:3000/posts?id=` + this.categoryFilter
      )
      this.items = res.data
    },
    async getCategory() {
      const res = await this.$axios.get('http://localhost:3000/category')
      this.categories = res.data
    },
    async refresh() {
      this.isLoading = true

      try {
        const res = await this.$axios.get(`http://localhost:3000/posts`)
        this.items = res.data

        if (this.items.length === 0) {
          this.isEmpty = true
        }
      } catch (err) {
        this.isError = true
      }

      this.isLoading = false
    }
  },
  async hapus() {
    const setuju = confirm('anda yakin?')
    if (!setuju) {
      return
    }
    const setuju2 = confirm('yakin ?')
    if (!setuju2) {
      return
    }

    this.$axios.delete('http://localhost:3000/posts/' + this.id).then((_) => {})
  },
  nameWithLang({ title, category_id }) {
    return `${title} — [${category_id}]`
  },
  computed: {
    filteredPosts: function() {
      var vm = this
      var categories = vm.categoryFilter

      return vm.items.filter(function(item) {
        return item.category_id
      })
    }
  }
}
</script>
<style>
.filter {
  font-family: arial;
  padding: 6px 6px;
  cursor: pointer;
  border-radius: 6px;
  transition: all 0.35s;
}
.filter.active {
  box-shadow: 0px 1px 3px 0px #00000026;
}

.filter:hover {
  background: lightgray;
}
</style>
