<template>
  <section class="section">
    <div class="columns is-mobile">
      <div class="card">
        <div class="card-image">
          <figure class="image is-4by3">
            <img :src="cat[0].catImage" alt="Placeholder image">
        </figure>
        </div>
        <div class="card-content container">
          <div class="media">
            <div class="media-content">
              <p class="title is-4">{{ cat[0].name }}</p>
            </div>
          </div>
          <div class="content">
            {{ cat[0].description }}
            <br>
          </div>
            <p>Temparment: {{ cat[0].temperament }}</p>
            <p>Origin: {{ cat[0].origin }}</p>
            <p>Life Spane {{ cat[0].lifeSpan }}</p>
            <status-level :cat="cat[0]" :catDefaults="catDefaults" :defaultLevel='defaultLevel'></status-level>
            <p>Other photos</p>
            <ul >
              <li v-for="image in cat[0].catImages" style="display:inline-block">
                <img :src="image.url" style=" width:200px;height:180px;">
              </li>
            </ul>
        </div>
        <quiz :cats="cat" ></quiz>
  </div>
</div>
</section>
</template>

<script>
import StatusLevel from '~/components/StatusLevel'
import axios from 'axios'
import Quiz from '~/components/Quiz'
export default {
  components: {
    StatusLevel,
    Quiz
  },
  async asyncData( context ){
    const { breed_id }  = context.query
    const response = await axios.get(`https://api.thecatapi.com/v1/images/search?breed_id=${breed_id}&limit=7`,
    {headers: { "x-api-key": 'c695ae68-432c-4c93-a1d7-a0b0b857c289' }})
    const { data } = response
    const [ breed = null ]= data[0].breeds
    if(breed){
      let images = ''
      images = data.slice(1, 7)

      const tempData = await axios.get('https://api.thecatapi.com/v1/breeds?limit=50')
      let random = Math.round( Math.random() * 45)
      return {
        cat: [ 
          {
          name: breed ? breed.name: 'Noname',
          temperament: breed ? breed.temperament: 'undefined',
          origin: breed ? breed.origin: 'undefined',
          lifeSpan: breed ? breed.life_span: 'undefined',
          wikipedia_url: breed ? breed.wikipedia_url: 'undefined',
          description: breed ? breed.description: 'undefined',         
          catImage: data ? data[0].url: 'undefined',
          adaptability: breed ? breed.adaptability: 0,
          affectionLevel: breed ? breed.affection_level: 0,
          childFriendly: breed ? breed.child_friendly: 0,
          grooming: breed ? breed.grooming : 0,
          intelligence: breed ? breed.intelligence: 0,
          healthIssues: breed ? breed.health_issues: 0,
          socialNeeds: breed ? breed.social_needs: 0,
          strangerFriendly: breed ? breed.stranger_friendly: 0,
          catImages: images,
        },
        {
        otherCatsForQuiz: tempData.data.slice(random, (random + 3)) 
        }
        ],
      }
    }
  },
  data(){
    return {
      defaultLevel: 5,
      catDefaults: {
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
      this.catDefaults.friendlyDefaultLevel = this.defaultLevel - this.cat[0].childFriendly
      this.catDefaults.affectionDefaultLevel = this.defaultLevel - this.cat[0].affectionLevel
      this.catDefaults.adaptabilityDefaultLevel = this.defaultLevel - this.cat[0].adaptability
      this.catDefaults.groomingmDefaultLevel = this.defaultLevel - this.cat[0].grooming
      this.catDefaults.intelligenceDefaultLevel = this.defaultLevel - this.cat[0].intelligence
      this.catDefaults.healthIssuesDefaultLevel = this.defaultLevel - this.cat[0].healthIssues
      this.catDefaults.socialNeedsDefaultLevel = this.defaultLevel - this.cat[0].socialNeeds
      this.catDefaults.strangerFriendlyDefaultLevel = this.defaultLevel - this.cat[0].strangerFriendly
    },
  },
}
</script>
