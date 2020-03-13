<template>
  <v-container>
    <v-card class="mx-auto" max-width="344">
      <form>
        <h3>Edit Post</h3>
        <v-text-field v-model="item.title"   label="Title"></v-text-field>
        <v-text-field v-model="item.content"   label="Content"></v-text-field>
        <v-text-field
          v-model="item.category_id"
          :name="category_id"
          :type="text"
          label="ID Kategori"
        ></v-text-field>
        <v-spacer></v-spacer>
        <v-btn color="success" @click.prevent="save">SEND</v-btn>
      </form>
    </v-card>
  </v-container>
</template>


<script>
// import MyNav from '~/components/my-nav'

export default {
  // components: { MyNav },
  data() {
    return {
      item: {},
      id: this.$route.params.id
    }
  },
  mounted() {
    this.getDetailPost()
  },
  methods: {
    getDetailPost() {
      this.$axios
        .get('http://localhost:3000/posts/' + this.$route.params.id)
        .then((res) => {
          this.item = res.data
        })
    },
    save() {
      this.$axios
        .patch(
          'http://localhost:3000/posts/' + this.$route.params.id,
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
