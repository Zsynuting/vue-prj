<template>
	<div>
		<div>
		<span class='float-cell'>
			<CalendarHeader v-for="item in weekdays" :weekday="item" />
			<CalendarCell v-for="dateItem in allDates" :date="dateItem" :date-cell="dateItem" />
			<div class='clear-float'></div>
		</span>
		</div>
	</div>
</template>

<script>
	import CalendarHeader from './calendarheader'
	import CalendarCell from './calendarcell'


	export default{
		props: ["selectedDate"],
		data: function(){
			var now = new Date(),
				obj = {
					weekdays: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
					minDate: new Date(0, 1, 1),
					maxDate: new Date(9999, 12, 31),
					currentDate: null,
					startDate: null,
					endDate: null,
					allDates: []
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
			CalendarHeader: CalendarHeader,
			CalendarCell: CalendarCell
		}
	}

</script>

<style scoped>
	.float-cell{
		float: left;
		width: 336px;
	}
	.clear-float{
		clear: both;
	}
</style>