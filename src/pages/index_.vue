<template>
  <my-select v-model="selected" :options="myOptions" />
</template>

<script>
// export default {
// 	name: 'PageIndex'
// }
// import tableData from 'assets/table-data'

// import {QZxh} from '../components/QZxh'

import MySelect from '../components/MySelect'


export default {
    data () {
      return {
        selected: null,
        myOptions: []
      }
    },

    components: { MySelect }
  }

</script>
