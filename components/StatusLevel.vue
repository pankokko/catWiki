<template>
  <div>
    <div>
      <p>Adaptability </p>
      <b-taglist v-if="cat.adaptability >= 1">
        <b-tag v-for="n of cat.adaptability" :key="n" type="is-dark"></b-tag>
        <b-tag v-for="n of catDefaults.adaptabilityDefaultLevel" :key="n" type="is-light"></b-tag>        
      </b-taglist>
      <b-taglist v-if="cat.adaptability === 0">
          <b-tag v-for="n of defaultLevel" :key="n" type="is-light"></b-tag>        
      </b-taglist>
      </div>
    <div>
      <p>AffectionLevel</p>
      <b-taglist v-if="cat.affectionLevel >= 1">
        <b-tag v-for="n of cat.affectionLevel" :key="n" type="is-dark"></b-tag>
        <b-tag v-for="n of catDefaults.affectionDefaultLevel " :key="n" type="is-dark"></b-tag>
      </b-taglist>
      <b-taglist v-if="cat.affectionLevel === 0">
        <b-tag v-for="n of cat.affectionLevel" :key="n" type="is-dark"></b-tag>
        <b-tag v-for="n of catDefaults.affectionDefaultLevel " :key="n" type="is-light"></b-tag>
      </b-taglist>
    </div>
    <div>
      <p>ChildFriendly</p>
      <b-taglist v-if="cat.childFriendly >= 1">
        <b-tag v-for="n of cat.childFriendly" :key="n" type="is-dark"></b-tag>
        <b-tag v-for="n of catDefaults.friendlyDefaultLevel " :key="n" type="is-light"></b-tag>
      </b-taglist>
        <b-taglist v-else-if="cat.childFriendly === 0">
        <b-tag v-for="n of catDefaults.friendlyDefaultLevel " :key="n" type="is-light"></b-tag>
      </b-taglist>
    </div>
    <div>
      <p>Grooming</p>
      <b-taglist v-if="cat.grooming >= 1">
        <b-tag v-for="n of cat.grooming" :key="n" type="is-dark"></b-tag>
        <b-tag v-for="n of catDefaults.groomingmDefaultLevel" :key="n" type="is-light"></b-tag>
      </b-taglist>
        <b-taglist v-else-if="cat.childFriendly === 0">
        <b-tag v-for="n of catDefaults.groomingmDefaultLevel" :key="n" type="is-light"></b-tag>
      </b-taglist>
    </div>
    <div>
    <p>Intelligence</p>
    <b-taglist v-if="cat.intelligence >= 1">
      <b-tag v-for="n of cat.intelligence" :key="n" type="is-dark"></b-tag>
      <b-tag v-for="n of catDefaults.intelligenceDefaultLevel " :key="n" type="is-light"></b-tag>
    </b-taglist>
      <b-taglist v-else-if="cat.intelligence === 0">
      <b-tag v-for="n of catDefaults.intelligenceDefaultLevel " :key="n" type="is-light"></b-tag>
    </b-taglist>
  </div>
  </div>
</template>

<script>

export default {
    props: ["cat", "catDefaults", 'defaultLevel']
}
</script>