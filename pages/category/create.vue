
<template>
<v-container>
    <v-btn to="/category" color="red lighten-3">Back</v-btn>
    
    <v-card
        class="mx-auto"
        max-width="344"
    >  
    <v-card-title> ADD CATEGORY </v-card-title>
    <v-form
    ref="form"
    v-model="valid"
    lazy-validation>
    <v-text-field
      v-model="item.title"
      :name="title"
      :type="text"
      label="Category"
      required
    ></v-text-field>
     <v-spacer> </v-spacer>
      <v-btn color="red lighten-3" @click.prevent="kirim">SEND</v-btn>
    </v-form>

  </v-card>
</v-container>
</template>

<script>
export default {
  data() {
    return {
      valid: true,
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
