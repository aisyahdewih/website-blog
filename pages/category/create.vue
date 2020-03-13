
<template>
<v-container>
    <v-btn to="/category">Back</v-btn>
    
    <v-card
        class="mx-auto"
        max-width="344"
    >  
    
    <form>
      <h3>Add Category</h3>
       <v-text-field
            v-model="item.title"
            :name="title"
            :type="text"
            label="Kategori"
            ></v-text-field>
      <v-spacer> </v-spacer>
      <v-btn color="success" @click.prevent="kirim">SEND</v-btn>
    </form>
  </v-card>
</v-container>
</template>

<script>
export default {
  data() {
    return {
      item: {}
    }
  },
  methods: {
    kirim() {
      this.$axios
        .post('http://localhost:3000/category', this.item)
        .then((_) => {
          this.$router.push('/category')
        })
    }
  }
}
</script>

<style></style>
