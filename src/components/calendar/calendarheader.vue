<template>
	<span>{{weekday}}</span>
</template>

<script>
	export default {
		props: ["weekday"]
	}
</script>

<style scoped>
	span {
		display: inline-block;
		width: 48px;
		height: 48px;
		text-align: center;
		line-height: 48px;
		font-size: 1em;
	}
</style>