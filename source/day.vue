<template lang='pug'>
	.day(
	v-bind:style='`width: ${width}px`'
	:class="{ 'showOddHours': sizeMedium }"
	)
		.measure
			.measureHour(v-for='(v, i) in 24 + 1')
				span.measureHourLabel {{ i > 0 ? i : 24 }}
		.timeLines
			.timeLine(v-for='(range, i) in day.people')
				.timeFill(
				v-bind:style="`left: ${range.from}%; right: ${100 - range.to}%;`"
				v-bind:title="`${people[i].firstName} ${people[i].lastName}`"
				)
				.hours
					.hour(v-for='i in 24 + 1')
						.hourLabel
		.summary
			.timeFill(
			v-bind:style="`left: ${match.from}%; right: ${100 - match.to}%;`"
			title='Summary'
			)
</template>
<style lang='sass' scoped>
@import 'settings'
.day
	position: relative
	flex-shrink: 0
	&.showOddHours
		.measureHour
			&:nth-child(odd)
				.measureHourLabel
					visibility: hidden
.measure
	display: flex
	flex-flow: row
	justify-content: space-between
	position: absolute
	top: -1rem
	width: 100%
.measureHour
	position: relative
.measureHourLabel
	position: absolute
	transform: translateX(-50%)
	text-align: center
	color: lightgray
	font-size: 0.7rem
	font-weight: 100
.timeLine
	position: relative
	height: 3rem
	margin-bottom: 0.25rem
	@each $color in $colors
		$i: index($colors, $color)
		&:nth-child(#{$i})
			.timeFill
				background-image: linear-gradient(to right, nth($color, 1), nth($color, 2))
.summary
	position: relative
	height: 1rem
	margin-top: 2rem
	margin-bottom: 1rem
.timeFill
	$size: 40%
	position: absolute
	top: (100% - $size) / 2
	z-index: 2
	height: $size
	background-color: lightgray
	background-image: linear-gradient(to right, #8e8e93, #68686e)
	border-radius: 2px
.hours
	position: relative
	z-index: 1
	display: flex
	flex-flow: row
	justify-content: space-between
	width: 100%
	height: 100%
.hour
	position: relative
	height: 100%
.hourLabel
	$size: 35%
	top: (100% - $size) / 2
	height: $size
	position: absolute
	width: 1px
	background: lightgray
	transform: translateX(-50%)
</style>
<script>
export default {
	name: 'day',
	props: [
		'day',
		'people',
		'width',
	],
	computed: {
		sizeMedium() {
			return Boolean(this.width < 400)
		},
		match() {
			return this.day.match
		},
	},
}
</script>
