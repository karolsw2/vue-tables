<template lang='pug'>
	.TableManager(:style='style')
		SmartMenu(@colorChanged='setColor')
			.button(v-on:click='pushTable') New table
		.TableManager__tables
			SmartTable(v-for='(table, index) in tables' :key='table.id')
				.button.button--red.button--icon(v-on:click='deleteTable(index)') 
						p delete
</template>

<script>
import SmartMenu from '@/components/SmartMenu'
import SmartTable from '@/components/SmartTable'

export default {
	name: 'TableManager',
	data () {
		return {
			style: {
				background: '#fff'
			},
			nextTableId: 1,
			tables: [{id: 0}]
		}
	},
	methods: {
		setColor: function (color) {
			this.style.background = color
		},
		pushTable: function () {
			this.tables.push({id: this.nextTableId++})
			var tableManager = document.getElementsByClassName('TableManager')[0]
			for (let i = 0; i < tableManager.scrollHeight; i++) {
				setTimeout(() => {
					tableManager.scrollTop += 1
				}, 1 + (2 / i))
			}
		},
		deleteTable: function (index) {
			this.tables.splice(index, 1)
		}
	},
	components: {SmartMenu, SmartTable}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang='stylus' scoped>
	.TableManager
		overflow-y auto
		background #ffffff
		height 100vh
		transition all 0.12s
		&__tables
			margin-top 50px
			overflow-y auto
</style>
