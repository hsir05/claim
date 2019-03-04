<template>
	<view>
		<view class="uni-padding-wrap">
			<form @submit="formSubmit" @reset="formReset">
				<view>
					<view class="uni-title">物品名称</view>
					<view class="uni-list">
						<view class="uni-list-cell">
							<input class="uni-input" name="articleName" placeholder="请填写物品名称" />
						</view>
					</view>
				</view>
				<view>
					<view class="uni-title">位置</view>
					<view class="uni-list">
						<view class="uni-list-cell">
							<input class="uni-input" name="lostLocation" placeholder="请填写丢失物品的位置" />
						</view>
					</view>
				</view>
				<view>
					<view class="uni-title">请填写物品描述</view>
					<view class="uni-textarea" auto-height>
						<textarea name="articleDesc" placeholder="请填写丢失物品描述"/>
					</view>
				</view>
				<view class="uni-title">捡到日期</view>
				<view class="uni-list">
					<view class="uni-list-cell">
						<view class="uni-list-cell-left">当前选择</view>
						<view class="uni-list-cell-db">
							<picker mode="date" :value="date" :start="startDate" :end="endDate" @change="bindDateChange">
								<view class="uni-input">{{date}}</view>
							</picker>
						</view>
					</view>
				</view>
				<view>
					<view class="uni-title">联系人姓名</view>
					<view class="uni-list">
						<view class="uni-list-cell">
							<input class="uni-input" name="ownerName" placeholder="请填写联系人姓名" />
						</view>
					</view>
				</view>
				<view>
					<view class="uni-title">联系电话</view>
					<view class="uni-list">
						<view class="uni-list-cell">
							<input class="uni-input" name="ownerPhone" placeholder="请填写联系电话" />
						</view>
					</view>
				</view>
				
				<view class="uni-common-mt">
					<view class="demo demo-border " v-if="imageSrc.length > 0">
						<view v-for="(item, index) in imageSrc" :key="item" class="del-wrop">
							<image :src="item"   class="image" mode="widthFix"></image>
							<view class="del" @click="delImg(index)">X</view>
						</view>
					</view>
					<view class="demo" v-if="imageSrc.length < 3">
						<block >
							<view class="uni-hello-addfile" @click="chooseImage">+ 选择图片</view>
						</block>
					</view>
				</view>
				
				<view class="uni-btn-v uni-common-mt">
					<button class="btn-submit" formType="submit" :loading="loading" type="primary">提交</button>
					<button type="default" :loading="loading" formType="reset">重置</button>
				</view>
			</form>
		</view>
	</view>
</template>
<script>
	const requestUrl = 'https://unidemo.dcloud.net.cn/ajax/echo/text?name=uni-app'
	const duration = 2000
	
	//来自 graceUI 的表单验证， 使用说明见手册 http://grace.hcoder.net/doc/info/73-3.html
	var  graceChecker = require("../../common/graceChecker.js");
	export default {
		data() {
			const currentDate = this.getDate({
				format: true
			})
			return {
				date: currentDate,
				title: 'request',
				loading: false,
				imageSrc: ['http://119.29.251.125:8082/imgUpload/bb0209d5fe5ac-d550a030ce8ee.png',"http://119.29.251.125:8082/imgUpload/55ddd67f5c6ef-cc28928d3f6ef.jpg"],
				res: ''
			}
		},
		computed: {
			startDate() {
				return this.getDate('start');
			},
			endDate() {
				return this.getDate('end');
			}
		},
		methods: {
			formSubmit: function (e) {
				//将下列代码加入到对应的检查位置
				//定义表单规则
				var rule = [
					{name:"articleName", checkType : "string", checkRule:"1,10",  errorMsg:"物品名称应为1-10个字符"},
					{name:"lostLocation", checkType : "string", checkRule:"1,30",  errorMsg:"请填写丢失物品的位置"},
					{name:"articleDesc", checkType : "string", checkRule:"1,30", errorMsg:"请填写物品描述"}, 
					{name:"ownerName", checkType : "string", checkRule:"1,10", errorMsg:"请填写联系人"},
					{name:"ownerPhone", checkType : "string", checkRule:"11", errorMsg:"请填写正确格式的联系方式"},

				];
				//进行表单检查
				var formData = e.detail.value;
				var checkRes = graceChecker.check(formData, rule);
				if(checkRes){
					this.loading = true
					formData.articlePhotos = [...this.imageSrc]
					formData.lostTime = this.date
					console.log(formData);
					return false
					uni.request({
						url: requestUrl,
						dataType: 'text',
						data: {
							noncestr: Date.now()
						},
						success: (res) => {
							console.log('request success', res)
							uni.showToast({
								title: '请求成功',
								icon: 'success',
								mask: true,
								duration: duration
							});
							this.res = '请求结果 : ' + JSON.stringify(res);
						},
						fail: (err) => {
							console.log('request fail', err);
							uni.showModal({
								content: err.errMsg,
								showCancel: false
							});
						},
						complete: () => {
							this.loading = false;
						}
					});
				}else{
					uni.showToast({ title: graceChecker.error, icon: "none" });
				}
			},
			formReset: function (e) {
				console.log("清空数据")
				formData.articleName = ''
				formData.lostLocation = ''
				formData.articleDesc = ''
				formData.ownerName = ''
				formData.ownerPhone = ''
				formData.articlePhotos = []
				formData.lostTime = ''
				this.imageSrc = []
			},
			bindDateChange: function(e) {
				this.date = e.target.value
			},
			delImg(index) {
				this.imageSrc.splice(index, 1)
			},
			chooseImage: function() {
				uni.chooseImage({
					count: 1,
					sizeType: ['compressed'],
					sourceType: ['album'],
					success: (res) => {
						console.log('chooseImage success, temp path is', res.tempFilePaths[0])
						var imageSrc = res.tempFilePaths[0]
						uni.uploadFile({
							url: 'http://119.29.251.125:8082/imgUpload',
							filePath: imageSrc,
							fileType: 'image',
							name: 'data',
							success: (res) => {
								console.log(JSON.parse(res.data).data)
								if (res.statusCode === 200) {
									let dat = JSON.parse(res.data).data[0]
									this.imageSrc.push(dat)
									uni.showToast({
										title: '上传成功',
										icon: 'success',
										duration: 1000
									})
								}
								
							},
							fail: (err) => {
								console.log('uploadImage fail', err);
								uni.showModal({
									content: err.errMsg,
									showCancel: false
								});
							}
						});
					},
					fail: (err) => {
						console.log('chooseImage fail', err)
					}
				})
			},
			getDate(type) {
				const date = new Date();
				let year = date.getFullYear();
				let month = date.getMonth() + 1;
				let day = date.getDate();

				if (type === 'start') {
					year = year - 60;
				} else if (type === 'end') {
					year = year + 2;
				}
				month = month > 9 ? month : '0' + month;;
				day = day > 9 ? day : '0' + day;
				return `${year}-${month}-${day}`;
			}
		}
	}
</script>

<style>
	.image {
		width: 100upx;
	}
	
	.demo {
		background: #FFF;
		padding: 20upx;
	}
	.demo-border{
		border-bottom: 1upx solid #F4F5F6;
		margin-bottom: 5px;
	}
	.del-wrop{
		position: relative;
		display: inline-block;
		padding: 15upx;
	}
	.del{
		width: 35upx;
		height: 35upx;
		lighting-color: 35upx;
		background-color: #DD524D;
		color: white;
		font-size: 20upx;
		text-align: center;
		border-radius: 5upx;
		position: absolute;
		top: 0;
		right: 0;
	}
</style>

