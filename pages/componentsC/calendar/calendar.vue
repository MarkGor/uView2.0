<template>
	<view class="u-page">
		<u-navbar
			title="日历"
			@leftClick="navigateBack"
			safeAreaInsetTop
			fixed
			placeholder
		></u-navbar>
		<u-cell-group>
			<u-cell
				@click="showCalendar(index)"
				:title="item.title"
				v-for="(item, index) in list"
				:key="index"
				isLink
			>
				<image
					slot="icon"
					class="u-cell-icon"
					:src="item.iconUrl"
					mode="widthFix"
				></image>
			</u-cell>
		</u-cell-group>
		<u-calendar
			:show="show1"
			@confirm="confirm"
			@close="close"
		></u-calendar>
		<u-calendar
			:show="show2"
			mode="multiple"
			@confirm="confirm"
			@close="close"
		></u-calendar>
		<u-calendar
			:show="show3"
			mode="range"
			@confirm="confirm"
			@close="close"
		></u-calendar>
		<u-calendar
			:show="show4"
			mode="range"
			@confirm="confirm"
			@close="close"
			color="#f56c6c"
			:defaultDate="customThemeDefaultDate"
		></u-calendar>
		<u-calendar
			:show="show5"
			mode="range"
			@confirm="confirm"
			@close="close"
			:defaultDate="customTextDefaultDate"
			startText="住店"
			endText="离店"
			confirmDisabledText="请选择离店日期"
			:formatter="formatter"
		></u-calendar>
		<u-calendar
			:show="show6"
			@confirm="confirm"
			@close="close"
			:maxDate="maxDate"
		></u-calendar>
		<u-calendar
			:show="show7"
			@confirm="confirm"
			@close="close"
			showLunar
		></u-calendar>
		<u-calendar
			:show="show8"
			@confirm="confirm"
			@close="close"
			mode="multiple"
			:defaultDate="defaultDateMultiple"
		></u-calendar>
	</view>
</template>
<script>
	export default {
		data() {
			const d = new Date()
			const year = d.getFullYear()
			let month = d.getMonth() + 1
			month = month < 10 ? `0${month}` : month
			const date = d.getDate()
			return {
				index: 0,
				show1: false,
				show2: false,
				show3: false,
				show4: false,
				show5: false,
				show6: false,
				show7: false,
				show8: false,
				customThemeDefaultDate: [`${year}-${month}-${date}`, `${year}-${month}-${date + 5}`], 
				customTextDefaultDate: [`${year}-${month}-${date}`],
				maxDate: `${year}-${month}-${date + 10}`,
				defaultDateMultiple: [`${year}-${month}-${date}`, `${year}-${month}-${date + 1}`, `${year}-${month}-${date + 2}`],
				list: [{
						title: '单个日期',
						iconUrl: 'https://cdn.uviewui.com/uview/demo/calendar/7.png'
					},
					{
						title: '多个日期',
						iconUrl: 'https://cdn.uviewui.com/uview/demo/calendar/8.png'
					},
					{
						title: '日期范围',
						iconUrl: 'https://cdn.uviewui.com/uview/demo/calendar/9.png'
					},
					{
						title: '自定义主题颜色',
						iconUrl: 'https://cdn.uviewui.com/uview/demo/calendar/15.png'
					},{
						title: '自定义文案',
						iconUrl: 'https://cdn.uviewui.com/uview/demo/calendar/14.png'
					},{
						title: '日期最大范围',
						iconUrl: 'https://cdn.uviewui.com/uview/demo/calendar/13.png'
					},{
						title: '显示农历',
						iconUrl: 'https://cdn.uviewui.com/uview/demo/calendar/5.png'
					},{
						title: '默认日期',
						iconUrl: 'https://cdn.uviewui.com/uview/demo/calendar/10.png'
					}
				]
			}
		},
		methods: {
			showCalendar(index) {
				this.index = index + 1
				this[`show${index + 1}`] = true
			},
			navigateBack() {
				uni.navigateBack();
			},
			confirm(e) {
				this[`show${this.index}`] = false
			},
			close() {
				this[`show${this.index}`] = false
			},
			formatter(day) {
				const d = new Date()
				let month = d.getMonth() + 1
				const date = d.getDate()
				if(day.month == month && day.day == date + 3) {
					day.bottomInfo = '有优惠'
					day.dot = true
				}
				return day
			}
		},
	}
</script>

<style lang="scss">
	.u-page {
		padding: 0;
	}
</style>
