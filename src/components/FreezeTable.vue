

<template>
	<q-table v-bind="$props" :tableClass="setClass">

	</q-table>
</template>

<script type="text/javascript">

import QTable from 'quasar'


export default {
	inheritAttrs: true,
	props: [
		"columns", 
		"data",
		"title", 
		"tableClass",
		"idx",
		"freeze_cols", 
		"freeze_backColor",
		"freeze_color"
	],
	mixin:[QTable],
	name: 'freeze-table',

	computed: {
		setClass () {
			return this.tableClass + " " + this.idx;
		},

	},

	methods: {
		ttt: function() {
			// alert(this.test1);
		},

		createFreeze: function() {
			var container = this.$el.getElementsByClassName(this.idx)[0];
			var table = container.getElementsByTagName('table')[0];
			var topHeaders = [].concat.apply([], table.querySelectorAll('thead th'));

			var headerContainer = [].concat.apply([], table.querySelectorAll('thead'));
			var rows = [].concat.apply([], table.querySelectorAll('tbody tr'));
			var fix_header = [];

			container.style.position = 'relative';

			//. set bgcolor and color
			var bgColor = this.freeze_backColor;
			var fColor = this.freeze_color;

			if (bgColor == undefined) 	bgColor = "#ffffff";
			if (fColor == undefined) 	fColor = "#333333";

			var fix_cols = [];
			
			//. cols fixed object
			for(var i = 0; i < rows.length; i++) {
				var r = rows[i].getElementsByTagName("td");
				for (var j = 0; j < this.freeze_cols; j++) {
					r[j].style.backgroundColor = bgColor;
					r[j].style.color = fColor;
					r[j].classList.add("freeze-cols");
					fix_cols.push(r[j]);
				}
			}

			//. header .
			for (var i = 0; i < topHeaders.length; i++) {
				topHeaders[i].style.backgroundColor = bgColor;
				topHeaders[i].style.color = fColor;
				topHeaders[i].style.transition = "none";
				topHeaders[i].style.zIndex = "10";
			}

			//. header fixed
			var h_container = document.createElement('div');
			h_container.classList.add("fix-header");

			var header_style = window.getComputedStyle(headerContainer[0]);

			h_container.style.height = header_style.height;
			h_container.style.backgroundColor = bgColor;
			h_container.style.color = fColor;
			container.appendChild(h_container);

			for (var i = 0; i < this.freeze_cols; i++) {				
				var tmp = document.createElement('div');
				var c_tmp = window.getComputedStyle(topHeaders[i], null);
				tmp.innerHTML = topHeaders[i].innerHTML;
				//. style
				tmp.style.width = c_tmp.width;
				tmp.style.height = c_tmp.height;
				tmp.style.textAlign = c_tmp.textAlign;
				tmp.style.border = c_tmp.border;
				tmp.style.font = c_tmp.font;
				tmp.style.padding = c_tmp.padding;
				tmp.style.color = c_tmp.color;
				tmp.style.paddingTop = "20px";
				tmp.style.float = "left";

				fix_header.push(tmp);
				h_container.appendChild(tmp);
			}

			table.addEventListener('resize', function(){
				alert('resize');
			});

			//. scroll event
			var that = this;
			container.addEventListener('scroll', function (e) {
				var x = container.scrollLeft;
				var y = container.scrollTop;

				for (var i = 0; i < topHeaders.length; i++) {
					topHeaders[i].style.transform = that.translate(0, y);
				}

				for (var i = 0; i < fix_cols.length; i++) {
					fix_cols[i].style.transform = that.translate(x, 0);
				}

				for (var i = 0; i < that.freeze_cols; i++) {
					var c_tmp = window.getComputedStyle(topHeaders[i]);
					fix_header[i].style.width = c_tmp.width;
				}
				h_container.style.transform = that.translate(x, y);
			});
		},
		translate: function(x, y) {
			return 'translate(' + x + 'px, ' + y + 'px)';
		}
	},

	mounted: function() {
		this.createFreeze();
	}

}

</script>

<style>


	.test-head {
		z-index: 10;
		opacity: 1;
		transition:none !important;
	}

	.freeze-cols {
		z-index: 2;
		/* opacity: 1; */
	}

	.fix-header {
		z-index : 100 !important;
		position: absolute !important;
		vertical-align: middle;
		top: 0 !important;
		left: 0 !important;
	}


	
</style>