<template>
	<div v-bind:class="['cell', {current: dateCell.isCurrent}, {currentmonth: dateCell.isCurrentMonth}]" >
		{{dateCell.date.getDate()}}
	</div>
</template>

<script>
	export default {
		props: ["dateCell"],
		data: function() {
			return {
				currentMonthClass: "not-current-month"
			}
		}
	}
</script>

<style scoped>
	.cell{
		display: inline-block;
		width: 48px;
		height: 48px;
		text-align: center;
		line-height: 48px;
		font-size: 1em;
		color: #aaa;
		cursor: pointer;
		box-sizing: border-box;
        -moz-box-sizing: border-box; 
        -webkit-box-sizing: border-box;
        border: 1px solid #fff;
	}
	.cell:hover{
		border: 1px solid;
	}
	.current{
		background-color: lightgrey;
	}
	.currentmonth{
		color: #000;
	}
</style>