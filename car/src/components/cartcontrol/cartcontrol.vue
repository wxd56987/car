<template>
	<div class="cartcontrol">
		<transition name="move">
			<div class="cart-descrease" v-show="food.count > 0" @click="decreaseCart">
				<transition name="roll">
					<span class="linner icon-remove_circle_outline" v-show="food.count > 0"></span>
				</transition>
			</div>
		</transition>
		<div class="cart-count" v-show="food.count > 0">{{ food.count }}</div>
		<div class="cart-add icon-check_circle" @click="addCart"></div>
	</div>
</template>

<script type="text/ecmascript-6">
	import Vue from 'Vue';

	export default {

		props: {
			food: {
				type: Object
			}
		},
		methods: {
			addCart() {
				if (!this.food.count) {
					// this.food.count = 1;// 只能通过引入Vue.set,赋值
					Vue.set(this.food, 'count', 1);
				} else {
					this.food.count++;
					let foodCount = this.food.count;
					Vue.delete(this.food, 'count');
					Vue.set(this.food, 'count', foodCount);
				}
			},
			decreaseCart() {
				if (this.food.count) {
					this.food.count--;
					let foodCount = this.food.count;
					Vue.delete(this.food, 'count');
					Vue.set(this.food, 'count', foodCount);
				}
			}
		}
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	.cartcontrol
		font-size: 0
		.cart-descrease
			display: inline-block
			padding: 6px
			.linner
				dosplay: inline-block
				font-size: 24px
				line-height: 24px
				color: rgb(0, 160, 220)	
				transform: rotate(0)
				&.roll-enter-active, &.roll-leave-active// 动画执行
				transition: all 0.5s linear
				&.roll-enter, &.roll-leave-to // 动画开始 结束
					transform: rotate(180deg)	
			&.move-enter-active, &.move-leave-active// 动画执行
				transition: all 0.5s linear
			&.move-enter, &.move-leave-to // 动画开始 结束
				opacity: 1
				transform: translate3D(24px, 0, 0)							
		.cart-count
			display: inline-block
			font-size: 10px
			vertical-align: top
			width: 12px
			padding-top: 6px
			line-height: 24px
			text-align: center
			color: rga(147, 153, 159)
		.cart-add
			display: inline-block
			padding: 6px
			font-size: 24px
			line-height: 24px
			color: rgb(0, 160, 220)
</style>