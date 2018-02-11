<template lang='pug'>
.view
	.humans
		.human(
		v-for='human in people'
		v-bind:title="`${human.firstName} ${human.lastName}`"
		)
			span {{ human.firstName[0] }}
			span {{ human.lastName[0] }}
	.time(v-on:click='zoomDays')
		.days: day(
		v-if='people'
		v-bind:day='day'
		v-bind:people='people'
		v-bind:width='zoom'
		v-for='day in days'
		v-bind:key='Math.random()'
		)
</template>
<style lang='sass' scoped>
@import 'settings'
.view
	display: flex
	flex-flow: row
.humans
	padding-top: 2rem
.human
	background-color: lightgray
	color: white
	width: 3rem
	height: 3rem
	margin-bottom: 0.25rem
	text-align: center
	line-height: 3rem
	border-radius: 3rem
	@each $color in $colors
		$i: index($colors, $color)
		&:nth-child(#{$i})
			background-image: linear-gradient(to bottom, nth($color, 1), nth($color, 2))
.time
	position: relative
	flex-grow: 1
	margin-left: 1rem
	overflow: auto
	padding-top: 2rem
.days
	display: flex
	flex-flow: row
	width: 100%
	position: relative
	left: 1rem
</style>
<script>
import people from './people'
import days from './days'
import day from './day'
export default {
	name: 'app-view',
	components: {
		day,
	},
	data() {
		return {
			people: people,
			days: days,
			zoom: 500,
		}
	},
	methods: {
		zoomDays() {
			return this.zoom == 500 ? this.zoom = 750 : this.zoom = 500
		}
	},
}
</script>
