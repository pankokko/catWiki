<template>
  <section class="section">
    <div class="columns is-mobile">
      <div class="card">
        <div class="card-image">
          <figure class="image is-4by3">
            <img :src="cat.catImage" alt="Placeholder image">
        </figure>
        </div>
        <div class="card-content">
          <div class="media">
            <div class="media-content">
              <p class="title is-4">{{ cat.name }}</p>
            </div>
          </div>
          <div class="content">
            {{ cat.description }}
            <br>
          </div>
            <p>Temparment: {{ cat.temperament }}</p>
            <p>Origin: {{ cat.origin }}</p>
            <p>Life Spane {{ cat.lifeSpan }}</p>
            <status-level :cat="cat" :catDefaults="catDefaults" :defaultLevel='defaultLevel'></status-level>
        </div>
  </div>
</div>
</section>
</template>

<script>
import Card from '~/components/Card'
import StatusLevel from '~/components/StatusLevel'
import axios from 'axios'
export default {
  name: 'HomePage',
  components: {
    Card,
    StatusLevel
  },
  async asyncData(){
    const response = await axios.get('https://api.thecatapi.com/v1/images/search?breed_id=beng',
    {headers: { "x-api-key": 'c695ae68-432c-4c93-a1d7-a0b0b857c289' }})
    const { data } = response
    const  breed = data[0].breeds[0]
    if(breed){
      return {
        cat: {
          name: breed ? breed.name: 'Noname',
          temperament: breed ? breed.temperament: 'undefined',
          origin: breed ? breed.origin: 'undefined',
          lifeSpan: breed ? breed.life_span: 'undefined',
          adaptability: breed ? breed.adaptability: 0,
          affectionLevel: breed ? breed.affection_level: 0,
          childFriendly: breed ? breed.child_friendly: 0,
          grooming: breed ? breed.grooming : 0,
          intelligence: breed ? breed.intelligence: 0,
          healthIssues: breed ? breed.health_issues: 0,
          socialNeeds: breed ? breed.social_needs: 0,
          strangerFriendly: breed ? breed.stranger_friendly: 0,
          infoUrl: breed ? breed.cfa_url: 'undefined',
          description: breed ? breed.description: 'undefined',         
          catImage: data ? data[0].url: 'undefined'
        }
      }
    }
  },
  data(){
    return {
      defaultLevel: 5,
      catDefaults :{
        friendlyDefaultLevel: 0,
        adaptabilityDefaultLevel: 0,
        affectionDefaultLevel: 0,
        groomingmDefaultLevel: 0,
        intelligenceDefaultLevel: 0,
        healthIssuesDefaultLevel: 0,
        socialNeedsDefaultLevel: 0,
        strangerFriendlyDefaultLevel: 0
      },
    }
  },
  created(){
    this.makeLevelLength()
  },
  methods: {
    makeLevelLength() {
      this.catDefaults.friendlyDefaultLevel = this.defaultLevel - this.cat.childFriendly
      this.catDefaults.affectionDefaultLevel = this.defaultLevel - this.cat.affectionLevel
      this.catDefaults.adaptabilityDefaultLevel = this.defaultLevel - this.cat.adaptability
      this.catDefaults.groomingmDefaultLevel = this.defaultLevel - this.cat.grooming
      this.catDefaults.intelligenceDefaultLevel = this.defaultLevel - this.cat.intelligence
    }
  },
}
</script>
