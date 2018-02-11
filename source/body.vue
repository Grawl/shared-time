<template lang='pug'>
	.body
		h1 {{ labels.name }}
		app-view
</template>
<script>
import appView from './view'
export default {
	name: 'app-body',
	components: {
		appView,
	},
	data() {
		return {
			labels: {
				name: 'Shared Time',
			},
		}
	},
}
</script>
