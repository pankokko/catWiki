<template>
  <div>
    <div>
      <p>Adaptability</p>
      <b-taglist v-if="cat.adaptability >= 1">
        <b-tag v-for="n of cat.adaptability" type="is-dark"></b-tag>
        <b-tag v-for="n of catDefaults.adaptabilityDefaultLevel" type="is-light"></b-tag>        
      </b-taglist>
      <b-taglist v-if="cat.adaptability === 0">
          <b-tag v-for="n of defaultLevel" type="is-light"></b-tag>        
      </b-taglist>
      </div>
    <div>
      <p>AffectionLevel</p>
      <b-taglist v-if="cat.affectionLevel >= 1">
        <b-tag v-for="n of cat.affectionLevel" type="is-dark"></b-tag>
        <b-tag v-for="n of catDefaults.affectionDefaultLevel "  type="is-dark"></b-tag>
      </b-taglist>
      <b-taglist v-if="cat.affectionLevel === 0">
        <b-tag v-for="n of cat.affectionLevel"  type="is-dark"></b-tag>
        <b-tag v-for="n of catDefaults.affectionDefaultLevel "type="is-light"></b-tag>
      </b-taglist>
    </div>
    <div>
      <p>ChildFriendly</p>
      <b-taglist v-if="cat.childFriendly >= 1">
        <b-tag v-for="n of cat.childFriendly" type="is-dark"></b-tag>
        <b-tag v-for="n of catDefaults.friendlyDefaultLevel"  type="is-light"></b-tag>
      </b-taglist>
        <b-taglist v-else-if="cat.childFriendly === 0">
        <b-tag v-for="n of catDefaults.friendlyDefaultLevel"  type="is-light"></b-tag>
      </b-taglist>
    </div>
    <div>
      <p>Grooming</p>
      <b-taglist v-if="cat.grooming >= 1">
        <b-tag v-for="n of cat.grooming"  type="is-dark"></b-tag>
        <b-tag v-for="n of catDefaults.groomingmDefaultLevel"  type="is-light"></b-tag>
      </b-taglist>
        <b-taglist v-else-if="cat.childFriendly === 0">
        <b-tag v-for="n of catDefaults.groomingmDefaultLevel"  type="is-light"></b-tag>
      </b-taglist>
    </div>
    <div>
    <p>Intelligence</p>
    <b-taglist v-if="cat.intelligence >= 1">
      <b-tag v-for="n of cat.intelligence"  type="is-dark"></b-tag>
      <b-tag v-for="n of catDefaults.intelligenceDefaultLevel "  type="is-light"></b-tag>
    </b-taglist>
      <b-taglist v-else-if="cat.intelligence === 0">
      <b-tag v-for="n of catDefaults.intelligenceDefaultLevel"  type="is-light"></b-tag>
    </b-taglist>
  </div>
    <div>
    <p>Health Issues </p>
    <b-taglist v-if="cat.healthIssues >= 1">
      <b-tag v-for="n of cat.healthIssues" type="is-dark"></b-tag>
      <b-tag v-for="n of catDefaults.healthIssuesDefaultLevel "  type="is-light"></b-tag>
    </b-taglist>
      <b-taglist v-else-if="cat.intelligence === 0">
      <b-tag v-for="n of catDefaults.healthIssuesDefaultLevel "  type="is-light"></b-tag>
    </b-taglist>
  </div>
    <div>
    <p>Social Needs</p>
    <b-taglist v-if="cat.socialNeeds >= 1">
      <b-tag v-for="n of cat.socialNeeds"  type="is-dark"></b-tag>
      <b-tag v-for="n of catDefaults.socialNeedsDefaultLevel "  type="is-light"></b-tag>
    </b-taglist>
      <b-taglist v-else-if="cat.socialNeeds === 0">
      <b-tag v-for="n of catDefaults.socialNeedsDefaultLevel "  type="is-light"></b-tag>
    </b-taglist>
  </div>
    <div>
    <p>Stranger Friendly</p>
    <b-taglist v-if="cat.strangerFriendly >= 1">
      <b-tag v-for="n of cat.strangerFriendly"  type="is-dark"></b-tag>
      <b-tag v-for="n of catDefaults.strangerFriendlyDefaultLevel "  type="is-light"></b-tag>
    </b-taglist>
      <b-taglist v-else-if="cat.strangerFriendly === 0">
      <b-tag v-for="n of catDefaults.strangerFriendlyDefaultLevel "  type="is-light"></b-tag>
    </b-taglist>
  </div>
  </div>
</template>

<script>

export default {
    props: ["cat", "catDefaults", 'defaultLevel'],
}
</script>