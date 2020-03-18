<template>
  <v-container>
     <v-btn to="/category" color="red lighten-3">Back</v-btn>
     <v-card class="mx-auto" max-width="344" color="red lighten-3">
        <v-card-title>ID : {{category.id}}</v-card-title>
        <v-card-subtitle> Category : {{category.title}}</v-card-subtitle>
        <v-spacer></v-spacer>
      </v-card>   
  </v-container>
 
</template>




<script>
export default {
  data() {
    return {
      category: {},
      id: this.$route.params.catId
    }
  },
  mounted() {
    this.$axios
      .get('http://localhost:3000/category/' + this.$route.params.catId)
      .then((res) => {
        this.category = res.data || {}
      })
  }
}
</script>

<style></style>
