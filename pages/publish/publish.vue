<template>
	<view class="uni-list">
		<view class="uni-list-cell" hover-class="uni-list-cell-hover">
			<view class="uni-list-cell-navigate uni-navigate-right" @click="goDetailPage('pub-article')">
				发布失物招领
			</view>
		</view>
		<view class="uni-list-cell" hover-class="uni-list-cell-hover">
			<view class="uni-list-cell-navigate uni-navigate-right" @click="goDetailPage('pub-notice')">
				发布寻物启事
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods:{
			goDetailPage(e) {
				let path = e.url ? e.url : e;
				let url = ~path.indexOf('platform') ? path : '/pages/publish/' + path;
				uni.navigateTo({
					url: url
				});
				return false;
			}
		}
	}
</script>

<style lang="scss">

</style>
