<template>
<section class="hero is-light is-large">
  <div class="hero-body">
    <div class="container">
      <h1 class="title">
        Search Cats
      </h1>
     <b-field label="Find a Bleed">
          <b-autocomplete
              v-model="keyword"
              :data="fillterSearch"
              icon="magnify"
              clearable
              @select=" (c) => selected = c"
              v-on:select="getLink(selected)"
              >
              <template slot="empty">No results found</template>
          </b-autocomplete>
        </b-field>
    </div>
  </div>
  <div>
  </div>
</section>
</template>
<script>
import axios from 'axios'
export default {

  async asyncData() {
    const response = await axios.get("https://api.thecatapi.com/v1/breeds", 
    {headers: { "x-api-key": 'c695ae68-432c-4c93-a1d7-a0b0b857c289' }}
    )
    const { data = null } = response
    if(data){
      let cats = []
      let filterCats = []
      data.forEach(c => {
        filterCats.push(c.name)
        cats.push({
          id: c.id,
          name: c.name
        })
      })
      return {
        cats,
        filterCats
      }
    }
  },
  data(){
    return {
        keyword: '',
        nativeSelect: '',
        link: '',
    }
  },
  computed: {
      fillterSearch() {
          return this.filterCats.filter((c) => {
              return c.toLowerCase().indexOf(this.keyword) >= 0           
      })
    },
  },

  methods: {
    // 検索項目で選ばれた猫の詳細ページにジャンプする関数
    getLink(value){
          this.cats.forEach((c) => {
          if (c.name === value) {
            this.$router.push({ path: 'show', query: { breed_id: c.id}})
          }
        })
    },
  }
}
</script>
