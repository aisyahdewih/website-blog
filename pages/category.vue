<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">Title</th>
          <th class="text-left">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in items" :key="item.title">
          <td>{{ item.title }}</td>
          <td> 
            
          </td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      items: []
    }
  },
  mounted() {
    this.fetchData()
  },
  methods: {
    async fetchData() {
      const res = await this.$axios.get(`http://localhost:3000/category`);
      this.items = res.data
    }
  }
}
</script>