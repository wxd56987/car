<template>
	<div class="title-line">
		<div class="line"></div>
		<div class="text">{{ lineMsg }}</div>
		<div class="line"></div>
	</div>
</template>

<script type="text/ecmascript-6">
	export default {
		props: {
			lineMsg: {
				type: String
			}
		}
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	.title-line
		display: flex
		width: 80%
		margin: 28px auto 24px
		.line
			flex: 1
			position: relative
			bottom: 6px
			border-bottom: 1px solid rgba(255, 255, 255, 0.2)							
		.text
			font-size: 14px
			padding: 0 12px
			font-weight: 700
</style>