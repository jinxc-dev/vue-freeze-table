<template>
	<q-page class="flex flex-center">
		<q-table
			title="Table Title"
			:data="tableData"
			:columns="columns"
			row-key="name"
			tableClass="fix-height"
			class="fix-width"
			:@click="event1"
		>
			<q-td slot="body-cell-desc" class='test_zxh' slot-scope="props" :props="props">
				{{ props.value }}
			</q-td>
			<q-td slot="body-cell-fat" slot-scope="props" :props="props">
				{{ props.value }}
			</q-td>
			
		<!-- <template slot="top-middle" slot-scope="props" :class="tableClass">			
		</template> -->
		</q-table>
		
	</q-page>

</template>

<style>
	.fix-height {
		height: 200px;
	}
	.fix-width {
		width: 500px;
	}
</style>

<script>

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

			scrollx : function(e){
				console.log('table-scroll');
				return;
			}


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

	mounted () {
		// this.target = this.$el.childNodes;
		// this.target.addEventListener('scroll', this.event1)

  	},

}

</script>
