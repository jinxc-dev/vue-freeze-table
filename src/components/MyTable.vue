
		<template>
		<q-table />
		</template>

<script>


import { QTable } from 'quasar'


  export default {
    props: ['value', 'options'],
    methods: {
      handleChange (newVal) {
        this.$emit('input', newVal)
      }
    },
    // name: 'MyTable',

    components: {
      QTable
    }
  }

</script>