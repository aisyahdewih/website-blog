 <template>
 
  <v-container fluid>
    <v-row no-gutters>
      <v-col>
        <div
          class="pa-2"
          outlined
          tile
        >
        <v-btn color="teal lighten-1" to="/post/create" flex="right">
          <v-icon small class="mr-2">mdi-add</v-icon>Add
        </v-btn> 
        </div>
      </v-col>
      <v-col md="auto">
        <div
          class="pa-2"
          outlined
          tile
        >
        <v-text-field
           v-model="query"
          label="Search"
          append-icon="mdi-magnify"
        ></v-text-field>
         <v-btn small outlined color="primary" @click="search">Search</v-btn>
        </div>
      </v-col>
    </v-row>   
    <v-row dense>
      <v-col v-for=" item in items" :key="item.title" :cols="item.flex">
        <v-card class="mx-auto" max-width="344">
          <v-img
            :src="item.src"
            class="white--text align-end"
            gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
            height="200px"
          ></v-img>

          <v-card-title v-text="item.title"></v-card-title>

          <v-card-subtitle v-text="item.content"></v-card-subtitle>

          <v-card-actions>
             <v-btn :to=" '/post/' + item.id + '/edit'">
              <v-icon small class="mr-2" color="teal lighten-1">mdi-pencil</v-icon> Edit
            </v-btn>
           <v-btn>
              <v-icon small @click="hapus(item.id)" color="teal lighten-1">mdi-delete</v-icon> Delete
           </v-btn>
            

            <v-spacer></v-spacer>

            <v-btn icon @click="show = !show">
              <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
            </v-btn>
          </v-card-actions>

          <v-expand-transition>
            <div v-show="show">
              <v-divider></v-divider>
              <v-card-text>{{item.content}}</v-card-text>
            </div>
          </v-expand-transition>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template> 


<script>
export default {
  data() {
    return {
      
      show: false,
      items: [],
      id: this.$route.params.id,
      query: '',
       isError: false,
      isEmpty: false,
      isLoading: false,
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