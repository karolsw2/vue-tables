<template lang='pug'>
	.SmartCell(:class='{"SmartCell--primary": primary}', :style='{background: color, padding: isEdited ? "5px 20px":"10px 20px"}', v-on:click='isEdited = true')
		div(v-if='!isEdited') {{staticText}}
		input.SmartCell__input.SmartCell__input--hidden(v-else, v-model='staticText', v-on:blur='isEdited = false', @keyup.enter='isEdited = false')
		slot(v-if='isEdited')
</template>

<script>

export default {
	name: 'SmartCell',
	props: ['text', 'primary', 'color'],
	data () {
		return {
			newText: this.text,
			isEdited: false
		}
	},
	computed: {
		staticText: {
			get: function () {
				return this.newText
			},
			set: function (newValue) {
				this.newText = newValue
			}
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang='stylus' scoped>
	borderRadius = 25px
	animationDuration = 0.1s

	.SmartCell
		@keyframes onShow
			0%
				opacity 0
				width 50%
			100%
				opacity 1
				width 100%
		display flex
		align-items center
		justify-content space-between
		cursor default
		margin 2px
		width 100%
		padding 10px 20px
		box-sizing border-box
		background #f5f5f5
		border-radius borderRadius
		transition all 0.5s
		animation-name onShow
		animation-duration animationDuration
		animation-timing-function ease-in
		transition all animationDuration
		&:hover
			opacity 0.7
		&--primary
			background #0084ff
			color #ffffff
		&__input
			text-align center
			min-width 0
			font-size 1em
			margin 2px
			padding 10px 20px
			border none
			width 100%
			background #f5f5f5
			box-sizing border-box
			border-radius borderRadius
			&--hidden
				background transparent
				margin 0
				padding 0
				color inherit			
</style>
