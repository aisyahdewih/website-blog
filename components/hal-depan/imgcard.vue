 <template>
 
  <v-container fluid>   
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
      search: '',
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
<!--<template>
  <v-card
    max-width="344"
  ><br>
    <v-img
      src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
      height="200px"
    ></v-img>

    <v-card-title>
      Top western road trips
    </v-card-title>

    <v-card-subtitle>
      1,000 miles of wonder
    </v-card-subtitle>

    <v-card-actions>
      <v-btn
        color="purple"
        text
      >
        Tulis Komentar
      </v-btn>

      <v-spacer></v-spacer>

      <v-btn
        icon
        @click="show = !show"
      >
        <v-icon>{{ show ? 'mdi mdi-border-color' : 'mdi mdi-comment-text-outline' }}</v-icon>
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>
          I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
        </v-card-text>
      </div>
    </v-expand-transition>
  </v-card>
</template> -->
<!--<script>
  // export default {
  //   data: () => ({
  //     show: false,
  //   }),
  // }
</script> -->