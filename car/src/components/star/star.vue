<template>
	<div class="star" :class="starType">
		<span v-for="itemClass in itemClasses" :class="itemClass" class="star-item"></span>
	</div>
</template>

<script type="text/ecmascript-6">
	const LENTH = 5;
	const CLS_ON = 'on';
	const CLS_HALF = 'half';
	const CLS_OFF = 'off';

	export default {
		props: {
			size: {
				type: Number
			},
			score: {
				type: Number
			}
		},
		computed: {
			starType() {
				return 'star-' + this.size;
			},
			itemClasses() {
				let result = [];
				let score = Math.floor(this.score * 2) / 2;
				let hasDecimal = score % 1 !== 0;
				let integer = Math.floor(score);
				for (let i = 0; i < integer; i++) {
					result.push(CLS_ON);
				}
				if (hasDecimal) {
					result.push(CLS_HALF);
				}
				while (result.length < LENTH) {
					result.push(CLS_OFF);
				}
				return result;
			}
		}
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin";
	.star
		font-size: 0
		.star-item
			display: inline-block
		&.star-48
			.star-item
				width: 20px
				height: 20px
				margin-right: 22px				
				&:last-child
					margin-right: 0
				&.on
					bg-image('star48_on')
					background-size: 20px 20px
				&.half
					bg-image('star48_half')
					background-size: 20px 20px
				&.off
					bg-image('star48_off')
					background-size: 20px 20px
		&.star-36
			.star-item
				width: 15px
				height: 15px
				margin-right: 6px
				&:last-child
					margin-right: 0
				&.on
					bg-image('star36_on')
					background-size: 15px 15px
				&.half
					bg-image('star36_half')
					background-size: 15px 15px
				&.off
					bg-image('star36_off')
					background-size: 15px 15px
		&.star-24
			.star-item
				width: 10px
				height: 10px
				margin-right: 3px
				&:last-child
					margin-right: 0
				&.on
					bg-image('star24_on')
					background-size: 10px 10px
				&.half
					bg-image('star24_half')
					background-size: 10px 10px
				&.off
					bg-image('star24_off')
					background-size: 10px 10px
</style>