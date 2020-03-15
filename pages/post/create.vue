
<template>
  <v-container>
    <v-btn to="/post" color="teal lighten-1">Back</v-btn>
    
    <v-card class="mx-auto" max-width="344">
        
      <form>
        <h3>Add Post</h3>
        <v-text-field v-model="item.title" :name="title" :type="text" label="Title"></v-text-field>
        <v-text-field v-model="item.content" :name="content" :type="textarea" label="Content"></v-text-field>
        <v-text-field
          v-model="item.category_id"
          :name="category_id"
          :type="textarea"
          label="ID Kategori"
        ></v-text-field>
        <v-spacer></v-spacer>
        <v-btn color="teal lighten-1" @click.prevent="kirim">SEND</v-btn>
      </form>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      item: {},
    }
  },
  methods: {
    kirim() {
      this.$axios.post('http://localhost:3000/posts', this.item).then((_) => {
        this.$router.push('/post')
      })
    }
  }
}
</script>

<style></style>
