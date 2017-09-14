<template>
	<select v-model="selectedMonth">
		<option v-for="month in months" v-bind:value="month.index">{{month.name}}</option>
	</select>
</template>

<script>
	export default {
		props: ["months", "selectedMonth"]
	}
</script>

<style>

</style>