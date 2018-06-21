<template>
	<q-page class="flex flex-center">
		<freeze-table
			row-key="name"
			title="This is Freeze Table"
			:data="tableData"
			:columns="columns"
			tableClass="fix-height"
			class="fix-width"
			freeze_cols="3"
			freeze_backColor="#aaaaaa"
			freeze_color = "white"
			idx="freeze"
		>
		</freeze-table>
		
	</q-page>

</template>

<style>
	.fix-height {
		height: 200px;
	}
	.fix-width {
		width: 700px;
	}
</style>

<script type="text/javascript">

import tableData from 'assets/table-data'
import FreezeTable from 'components/FreezeTable'


export default {
	inheritAttrs: true,
	data() {
		
		return {
			tableData,
			title: "Title",
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
			]

		}
	},
	computed: {
		tableClass () {
			console.log('tableClass');
			return 'fix-height'
		}, 
		getFixed (h) {
			// return 'div';
			return h('div');
		},
		event1(e) {
			console.log('scroll');
			return;
		}
	},

// mixin:[FreezeTable],
components: { FreezeTable },

	mounted () {
		// this.target = this.$el.childNodes;
		// this.target.addEventListener('scroll', this.event1)

  	},

}

</script>
