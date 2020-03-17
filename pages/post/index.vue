 <template>
  <v-container fluid>
    <v-row no-gutters>
      <v-col>
        <div class="pa-2" outlined tile>
          <v-btn color="teal lighten-1" to="/post/create" flex="right">
            <v-icon small class="mr-2">mdi-add</v-icon>Add
          </v-btn>
        </div>
      </v-col>
      <v-col md="auto">
        <div class="pa-2" outlined tile>
          <v-text-field v-model="query" label="Search" append-icon="mdi-magnify"></v-text-field>
          <v-btn small outlined color="primary" @click="search">Search</v-btn>
        </div>
      </v-col>
    </v-row>
    <v-container>
      <v-row dense>
        <v-col
          v-for=" item in items"
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
export default {
  components: {ListCard},
  data() {
    return {
      items: [],
      id: this.$route.params.id,
      query: '',
       isError: false,
      isEmpty: false,
      isLoading: false,
      pagination : {'sortBy': 'id', 'descending': true, 'rowsPerPage': -1}
    }
  },
  mounted() {
    this.refresh()
  },
  methods: {
    async search() {
       this.isLoading = true;
      try {
        const res = await this.$axios.get("http://localhost:3000/posts", {
          params: {
            q: this.query
          }
        });
        this.items = res.data;
        if (this.items.length === 0) {
          this.isEmpty = true;
        }
      } catch (err) {
        this.isError = true;
      }
      this.isLoading = false;
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
  computed: {
    filteredPosts: function() {
      return this.items.filter(item => {
        return item.title.match(this.search);
      });
    }
  }
}
</script>