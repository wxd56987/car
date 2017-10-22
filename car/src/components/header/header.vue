<template>
	<div class="header">
		<div class="content-wrapper">
			<div class="avatar">
				<img width="64" height="64" :src="seller.avatar">
			</div>
			<div class="content">
				<div class="title">
					<span class="brand"></span>
					<span class="name">{{ seller.name }}</span>
				</div>
				<div class="description">
					{{ seller.description }}/{{ seller.deliveryTime }}分钟送达
				</div>
				<div v-if="seller.supports" class="supports">
					<span class="icon" :class="ClassMap[seller.supports[0].type]"></span>
					<span class="text">{{ seller.supports[0].description }}</span>
				</div>
			</div>
			<div v-if="seller.supports" class="support-count" @click="showDetail">
				<span class="count">{{ seller.supports.length }}个</span>
				<i class="icon-keyboard_arrow_right"></i>
			</div>
		</div>
		<div class="bulletin-wrapper" @click="showDetail">
			<span class="bulletin-title"></span><span class="bulletin-text">{{ seller.bulletin }}</span>
			<i class="icon-keyboard_arrow_right"></i>
		</div>
		<div class="backgroud">
			<img :src="seller.avatar" width="100%" height="100%">
		</div>
		<transition name="fade">
			<div v-show="detailShow" class="detail">
				<div class="detail-wrapper clearfix">
					<div class="detail-main">
						<h1 class="name">{{ seller.name }}</h1>
						<div class="star-wrapper">
							<star :size="48" :score="seller.score"></star>
						</div>
						<div class="line-wrapper">
							<liner :lineMsg="msg[0]"></liner>
						</div>
						<ul v-if="seller.supports" class="supports">
							<li class="supports-item" v-for="item in seller.supports">
								<span class="icon" :class="ClassMap[item.type]"></span>
								<span class="text">{{ item.description }}</span>
							</li>
						</ul>
						<div class="line-wrapper">
							<liner :lineMsg="msg[1]"></liner>
						</div>
						<div class="bulletin">
							<p class="content">{{ seller.bulletin }}</p>
						</div>
					</div>
				</div>
				<div class="detai-close" @click="hideDetail">
					<i class="icon-close"></i>
				</div>
			</div>
		</transition>
	</div>
</template>

<script type="text/ecmascript-6">
	import star from '../../components/star/star.vue';
	import liner from '../../components/line/liner.vue';

	export default {
		props: {
			seller: {
				type: Object
			}
		},
		data() {
			return {
				msg: ['优惠信息', '商家公告'],
				detailShow: false
			};
		},
		methods: {
			showDetail() {
				this.detailShow = true;
			},
			hideDetail() {
				this.detailShow = false;
			}
		},
		created() {
			this.ClassMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
		},
		components: {
			'star': star,
			liner
		}
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin";
	.header
		color: #fff
		position: relative
		background: rgba(7, 17, 27, 0.5)
		overflow: hidden
		.content-wrapper
			padding: 24px 12px 18px 24px
			box-sizing: border-box
			font-size: 0
			position: relative
			.avatar
				display: inline-block
			.content
				display: inline-block
				margin-left: 16px
				font-size: 12px
				.title
					margin: 2px 0 8px 0
					.brand
						display: inline-block
						vertical-align: top
						width: 30px
						height: 18px
						bg-image('brand');
						background-size: 30px 18px;
					.name
						margin-left: 6px
						font-size: 16px
						line-height: 18px
						font-weight: bold
				.description
					font-size: 12px
					margin-bottom: 10px
					line-height: 12px
				.supports
					.icon
						display: inline-block
						width: 12px
						height: 12px
						margin-right: 4px	
						vertical-align: top					
						&.decrease
							bg-image('decrease_1')
							background-size: 12px 12px
						&.discount
							bg-image('discount_1')
							background-size: 12px 12px
						&.guarantee
							bg-image('guarantee_1')
							background-size: 12px 12px
						&.invoice
							bg-image('invoice_1')
							background-size: 12px 12px
						&.special
							bg-image('special_1')
							background-size: 12px 12px
					.text
						font-size: 10px
						line-height: 12px
			.support-count
				position: absolute
				right: 12px
				bottom: 14px
				padding: 0 8px
				height: 24px
				line-height: 24px
				border-radius: 14px
				background: rgba(0, 0, 0, 0.2)
				text-align: center
				.count
					vertical-align: top
					font-size: 10px
				.icon-keyboard_arrow_right
					margin-left: 2px
					font-size: 10px
					line-height: 24px
		.bulletin-wrapper
			position: relative
			width: 100%
			height: 28px
			line-height: 28px
			padding: 0 22px 0 12px
			white-space: nowrap
			overflow: hidden
			text-overflow: ellipsis
			box-sizing: border-box
			background: rgba(7, 17, 27, 0.2)
			.bulletin-title
				display: inline-block
				vertical-align: top
				margin-top: 9px
				width: 22px 
				height: 12px
				bg-image('bulletin')
				background-size: 22px 12px
			.bulletin-text
				margin: 0 4px
				font-size: 10px
			.icon-keyboard_arrow_right
				position: absolute
				font-size: 10px
				right: 12px
				top: 11px
		.backgroud
			position: absolute
			top: 0
			left: 0
			width: 100%
			height: 100%
			z-index: -1				
			filter: blur(10px)
		.detail
			position: fixed
			z-index: 100
			top: 0
			left: 0
			width: 100%
			height: 100%
			overflow: auto
			background: rgba(7, 17, 27, 0.8)
			&.fade-enter-active, &.fade-leave-active 
				transition: opacity .5s			
			&.fade-enter, &.fade-leave-active 
				opacity: 0				
			.detail-wrapper
				min-height: 100%
				width: 100%
				.detail-main
					margin-top: 64px
					padding-bottom: 64px
					.name
						line-height: 16px
						text-align: center
						font-size: 16px
						font-weight: 700
					.star-wrapper
						text-align: center
						margin-top: 16px
						padding: 2px 0
					.supports
						width: 80%
						margin: 0 auto
						.supports-item
							padding: 0 12px
							margin-bottom: 12px
							font-size: 0
							&:last-child
								margin-bottom0
							.icon
								display: inline-block
								width: 16px
								height: 16px
								vertical-align: top
								margin-right: 6px
								&.decrease
									bg-image('decrease_2')
									background-size: 16px 16px
								&.discount
									bg-image('discount_2')
									background-size: 16px 16px
								&.guarantee
									bg-image('guarantee_2')
									background-size: 16px 16px
								&.invoice
									bg-image('invoice_2')
									background-size: 16px 16px
								&.special
									bg-image('special_2')
									background-size: 16px 16px
							.text
								line-height: 16px
								font-size: 12px
					.bulletin
						width: 80%
						padding: 0 12px
						margin: 0 auto
						box-sizing: border-box
						.content
							font-size: 12px
							line-height: 24px
							text-align: justify
			.detai-close
				position: relative
				width: 32px
				height: 32px
				margin: -64px auto 0
				clear: both
				font-size: 32px				
				
				
</style>