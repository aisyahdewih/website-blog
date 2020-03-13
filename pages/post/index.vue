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

          <v-card-subtitle v-text="item.content"></v-card-subtitle>

          <v-card-actions>
            <v-btn text>EDIT</v-btn>

            <v-btn color="purple" text>DELETE</v-btn>

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
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      items: []
    }
  },
  mounted() {
    this.refresh()
  },
  methods: {
    async search() {
      // SEARCH API
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
  }
}
</script>