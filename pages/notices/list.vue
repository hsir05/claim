<template>
	<view>
		<uni-card 
		    v-for="item in result"
			:key="item.id"
			is-full="true" 
			:title="item.articleName"  
			:extra="`发布时间:${item.createTime}`"
			:note="`捡到时间:${item.lostTime}`"
			:lostLocation="item.lostLocation"
			:content="item.articleDesc"
			:imgList="item.articlePhoto">
		</uni-card>
		<view class="pagin">
			<uni-pagination 
				show-icon="true" 
				total="30" 
				current="2">
			</uni-pagination>
		</view>
	</view>
</template>

<script>
	import uniCard from "@/components/uni-card.vue"
	import uniPagination from "@/components/uni-pagination.vue"
	export default {
		components: {uniCard,uniPagination},
		data() {
			return {
				result: [
					{
						lostLocation: '甘肃省兰州市城关区庆阳路十字',
						id: 'sdfsdf333sdf24234243',
						articleName: '小马甲',
						lostTime: '2018.12.03',
						articleDesc: '一个棕色的钱包，主要物品有省份证，人民并币若干',
						articlePhoto:[],
						ownerName:'李元吉',
						ownerPhone:'138069845',
						createTime:'2018.12.12'
					}
				]
			};
		}
	}
</script>

<style lang="scss">
.pagin{
	background-color: white;
	padding: 10upx 0;
	margin: 20upx 0;
}
</style>
