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
	</view>
</template>

<script>
	import uniCard from "@/components/uni-card.vue"
	export default {
		components: {uniCard},
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

</style>
