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
					},
					{
						lostLocation: '甘肃省兰州市城关区庆阳路十字',
						id: 'sdfsdfsdf24234243',
						articleName: '钱包',
						lostTime: '2018.12.03',
						articleDesc: '一个棕色的钱包，主要物品有省份证，人民并币若干',
						articlePhoto:[
							'http://www.pptbz.com/pptpic/UploadFiles_6909/201203/2012031220134655.jpg',
						    'http://img5.miaopai.com/images/kaKyv8gZgX1dUETLuKMhZP3dlDaSlT9yl4JGCQ___c0r1_4.jpg',
						],
						ownerName:'李元吉',
						ownerPhone:'138069845',
						createTime:'2018.12.12'
					},
					{
						lostLocation: '甘肃省兰州市城关区庆阳路十字',
						id: 'sdffsdfsdf',
						articleName: '白色小狗',
						lostTime: '2018.12.03',
						articleDesc: '一个棕色的钱包，主要物品有省份证，人民并币若干',
						articlePhoto:[
							'http://www.pptbz.com/pptpic/UploadFiles_6909/201203/2012031220134655.jpg',
							'http://img5.miaopai.com/images/kaKyv8gZgX1dUETLuKMhZP3dlDaSlT9yl4JGCQ___c0r1_4.jpg',
							'http://img.zcool.cn/community/0179e9554bdad1000001bf729792d6.jpg@1280w_1l_2o_100sh.jpg',
						],
						ownerName:'李元吉',
						ownerPhone:'138069845',
						createTime:'2018.12.12'
					},
					{
						lostLocation: '甘肃省兰州市城关区庆阳路十字',
						id: 'sdffsdfsdf42424234',
						articleName: '笔记本电脑',
						lostTime: '2018.12.03',
						articleDesc: '一个棕色的钱包，主要物品有省份证，人民并币若干',
						articlePhoto:['http://www.pptbz.com/pptpic/UploadFiles_6909/201203/2012031220134655.jpg'],
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
	.desc-wrop{
		display: flex;
		align-items: center;
		justify-content: left;
		padding-top: 10px;
		padding-bottom: 10px;
		.desc-img{
			width: 33%;
			height: 100px;
		}
	}

</style>
