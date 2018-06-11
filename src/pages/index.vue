<template>
	<q-page class="flex flex-center">
		<q-table
			title="Table Title"
			:data="tableData"
			:columns="columns"
			row-key="name"
			tableClass="fix-height"

		>
		
		<!-- <template slot="top-middle" slot-scope="props" :class="tableClass">			
		</template> -->
		</q-table>
	</q-page>
</template>

<style>
	.fix-height {
		height: 200px;
	}
</style>

<script>
// export default {
// 	name: 'PageIndex'
// }
import tableData from 'assets/table-data'

export default {
	data() {
		return {
			tableData,
			columns: [
				{
					name: 'desc',
					required: true,
					label: 'Dessert (100g serving)',
					align: 'left',
					field: 'name',
					sortable: true
				},
				{ name: 'calories', label: 'Calories', field: 'calories', sortable: true },
				{ name: 'fat', label: 'Fat (g)', field: 'fat', sortable: true },
				{ name: 'carbs', label: 'Carbs (g)', field: 'carbs' },
				{ name: 'protein', label: 'Protein (g)', field: 'protein' },
				{ name: 'sodium', label: 'Sodium (mg)', field: 'sodium' },
				{ name: 'calcium', label: 'Calcium (%)', field: 'calcium', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) },
				{ name: 'iron', label: 'Iron (%)', field: 'iron', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) }
			],
		}
	},
	computed: {
		tableClass () {
			return 'fix-height'
		}
	},

}
</script>
