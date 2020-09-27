<template>
    <div>
        <b-message title="Correct Answer" type="is-info" aria-close-label="Close message" v-model="alert.status" v-if="alert.correct">
        <p>Watch more info of this breed</p>
        <p><a :href="wikipediaUrl">jump to Wikipedia</a></p>
        </b-message>
        <b-message title="Long Answer" type="is-warning" aria-close-label="Close message" v-model="alert.status" v-else-if="alert.inccorect">
        {{ alert.alertMessage }}
        </b-message>
    </div> 
</template>
<script>
export default {
    props:{
        alert: {
            type: Object,
            required: false,
            default: false,
        },
        wikipediaUrl: {
            type: String,
            required: false,
            default: ''
        }
    } 
}
</script>