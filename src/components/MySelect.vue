
		<template>
		  <q-select :value="value" :options="options" @change="handleChange" filter filter-placeholder="select"/>
		</template>

<script>


import { QSelect } from 'quasar'


  export default {
    props: ['value', 'options'],
    methods: {
      handleChange (newVal) {
        this.$emit('input', newVal)
      }
    },

    components: {
      QSelect
    }
  }

</script>