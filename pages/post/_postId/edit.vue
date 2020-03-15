<template>
  <v-container>
    <v-btn to="/post" color="teal lighten-1">Back</v-btn>
    <v-card class="mx-auto" max-width="344">
      <form>
        <h3>Edit Post</h3>
        <v-text-field v-model="item.title" :name="title" label="Title"></v-text-field>
        <v-text-field v-model="item.content" :name="content"  label="Content"></v-text-field>
        <v-text-field
          v-model="item.category_id"
          :name="category_id"
          :type="text"
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
      item: {}
    }
  },
  mounted() {
    this.getDetail()
  },
  methods: {
    getDetail() {
      this.$axios
        .get('http://localhost:3000/posts/' + this.$route.params.postId)
        .then((res) => {
          this.item = res.data || {}
        })
    },
    kirim() {
      this.$axios
        .patch(
          'http://localhost:3000/posts/' + this.$route.params.postId,
          this.item
        )
        .then((_) => {
          this.$router.push('/post')
        })
    }
  }
}
</script>

<style></style>

