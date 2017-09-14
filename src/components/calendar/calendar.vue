<template>
	<div class="calendar-container">
		<div>
			<div class='float-cell'>
				<div class="selector">
					<select v-model="selectedMonth" class="width: 30%">
						<option v-for="month in months" :value="month.index">{{month.name}}</option>
					</select>
				</div>
				<div class="selector">
				</div>
				<div class='clear-float'></div>
			</div>
			<span class='float-cell'>
				<span class="calendar-header" v-for="weekday in weekdays">{{weekday}}</span>
				<div v-bind:class="['cell', {current: dateItem.isCurrent}, {currentmonth: dateItem.isCurrentMonth}]" v-for="dateItem in allDates">
					{{dateItem.date.getDate()}}
				</div>
				<div class='clear-float'></div>
			</span>
		</div>
	</div>
</template>

<script>


	export default{
		props: ["selectedDate"],
		data: function(){
			var now = new Date(),
				obj = {
					weekdays: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
					minDate: new Date(0, 1, 1),
					maxDate: new Date(9999, 12, 31),
					currentDate: null,
					selectedMonth: null,
					selectedYear: null,
					startDate: null,
					endDate: null,
					allDates: [],
					months: [
					{
						name: "Jan",
						index: 0
					},					
					{
						name: "Feb",
						index: 1
					},
					{
						name: "Mar",
						index: 2
					},
					{
						name: "Apr",
						index: 3
					},
					{
						name: "May",
						index: 4
					},
					{
						name: "Jun",
						index: 5
					},
					{
						name: "Jul",
						index: 6
					},
					{
						name: "Aug",
						index: 7
					},
					{
						name: "Sep",
						index: 8
					},
					{
						name: "Oct",
						index: 9
					},
					{
						name: "Nov",
						index: 10
					},
					{
						name: "Dec",
						index: 11
					}
					]
				};
		 	obj.currentDate = this.$options.propsData.selectedDate ? 
		 		new Date(this.$options.propsData.selectedDate) : new Date(now.getFullYear(), now.getMonth(), now.getDate());

			var 
		 		currentMonth = obj.currentDate.getMonth(),
		 		currentYear = obj.currentDate.getFullYear(),
		 		isLeapYear = (currentYear % 4 == 0) && (currentYear % 100 != 0 || currentYear % 400 == 0),
		 		daysOfEachMonth = isLeapYear ? [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31] 
		 			: [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31],
		 		firstDayOfCurrentMonth = new Date(currentYear, currentMonth, 1),
		 		lastDayOfCurrentMonth = new Date(currentYear, currentMonth, daysOfEachMonth[currentMonth]),
		 		daysOfPrevMonth = firstDayOfCurrentMonth.getDay(),
		 		daysOfNextMonth = 6 - lastDayOfCurrentMonth.getDay();

		 	obj.startDate = new Date(firstDayOfCurrentMonth.getTime() - daysOfPrevMonth * 24 * 60 * 60 * 1000);
		 	obj.endDate = new Date(lastDayOfCurrentMonth.getTime() + daysOfNextMonth * 24 * 60 * 60 * 1000);
		 	obj.selectedYear = obj.currentDate.getFullYear();
		 	obj.selectedMonth = obj.currentDate.getMonth();
		 	
		 	
		 	var tempDate = new Date(obj.startDate);
		 	while(tempDate <= obj.endDate) {
		 		obj.allDates.push({
		 			date: new Date(tempDate.getTime()),
		 			isCurrent: tempDate.getTime() === obj.currentDate.getTime(),
		 			isCurrentMonth: tempDate.getMonth() == currentMonth
		 		});
		 		tempDate = new Date(tempDate.setDate(tempDate.getDate() + 1));
		 	} 
			return obj;

		},
		components: {
		}
	}

</script>

<style scoped>
	.calendar-container{
		width: 336px;
	}
	.float-cell{
		float: left;
		width: 336px;
	}
	.clear-float{
		clear: both;
	}
	.selector{
		float: left;
		display: inline-block;
		box-sizing: border-box;
        -moz-box-sizing: border-box; 
        -webkit-box-sizing: border-box;
		width: 50%
	}
	.calendar-header{
		display: inline-block;
		width: 48px;
		height: 48px;
		text-align: center;
		line-height: 48px;
		font-size: 1em;
	}
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