<template>
	<view class="content">
		<view class="dueto-header">
			<view class="dueto_left">
				<text class="active-text">全部</text>
				<text>10条</text>
			</view>
			<view class="dueto_right">
				<view class="dueto_right-item active-tab">全部</view>
				<view class="dueto_right-item">待办</view>
				<view class="dueto_right-item">已完成</view>
			</view>
		</view>
		<view class="dueto-content">
			<view class="dueto-list dueto--finished">
				<view class="dueto-list_checkbox">
					<view class="checkbox"></view>
				</view>
				<view class="dueto-list_content">我的待办事项!</view>
			</view>
		</view>
		<view class="create-dueto">
			<text class="iconfont icon-add"></text>
		</view>
		<view class="create-content">
			<view class="create-content-box">
				<view class="create-input">
					<input type="text" value="" placeholder="请输入您要创建的dueto" />
				</view>
				<view class="create-button">创建</view>	
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	@import "../../common/icon.css";
.dueto-header{
	display: flex;
	align-items: center;
	font-size: 12px;
	color: #333333;
	padding: 0 15px;
	height: 45rpx;
	box-shadow: -1px 1px 5px 0 rgba(0,0,0,0.1);
	background-color:#FFFFFF;
}
.dueto_left{
	width: 100%;
}
.active-text {
	font-size: 12px;
	color: #007AFF;
	padding-right: 10px;
}
.dueto_right {
	flex-shrink: 0;
	display: flex;
}
.dueto_right-item{
	padding: 0 5px;
}
	
.active-tab{
	color: #007AFF;
}

.dueto-content{
	position: relative;
	/* border: 1px solid green; */
}
.dueto-list{
	position: relative;
	display: flex;
	align-items: center;
	padding: 15px;
	margin: 15px;
	color: #0c3854;
	box-shadow: -1px 1px 5px 1px rgba(0,0,0,0.1), -1px 2px 1px 0 rgba(255,255,255) inset;
	border-radius: 10px;
	background:#cfebfd;
	overflow: hidden;
}
.dueto-list:after{
	position: absolute;
	content: '';
	top: 0;
	left: 0;
	bottom: 0;
	width: 5px;
	background: #91d1e8;
}
.dueto-list_checkbox{
	padding-right: 10px;
}
.checkbox{
	width: 20px;
	height: 20px;
	border-radius: 50%;
	background: #FFFFFF;
	box-shadow: 0 0 5px 1px rgba(0,0,0,0.1);
}
.dueto--finished .checkbox{
	background:#eee;
	position: relative;
}
.dueto--finished .checkbox:after{
	position: absolute;
	content: '';
	width: 10px;
	height: 10px;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	margin: auto;
	background: #CFEBFD;
	border-radius: 50%;
	box-shadow: 0 0 2px 0 rgba(0,0,0,0.1) inset;
}
.dueto--finished .dueto-list_content{
	color: #999999;
}
.dueto--finished.dueto-list:before{
	content: '';
	position: absolute;
	top: 0;
	bottom: 0;
	left: 40px;
	right: 10px;
	height: 2px;
	margin: auto 0;
	background:#bdcdd8;
}
	
.dueto--finished.dueto-list:after{
	background: #C0C0C0;
}

.create-dueto{
	position: fixed;
	display: flex;
	justify-content: center;
	align-items: center;
	left: 0;
	right: 0;
	margin: 0 auto;
	bottom: 20px;
	width: 50px;
	height: 50px;
	border-radius: 50%;
	background-color: #deeff5;
	box-shadow: -1px 1px 5px 2px rgba(0,0,0,0.1), -1px 1px 1px 0 rgba(255,255,255) inset;
}
.icon-add{
	font-size: 25px;
	color: #add8e6;
}

.create-content{
	position: fixed;
	bottom: 95px;
	left: 20px;
	right: 20px;
}
.create-content-box{
	display: flex;
	align-items: center;
	padding:0 15px;
	padding-right: 0;
	border-radius: 50px;
	background-color:#DEEFF5;
	box-shadow: -1px 1px 5px 2px rgba(0,0,0,0.1),-1px 1px 1px 0 rgba(255,255,255) inset;
}
.create-input{
	width: 100%;
	padding-right: 15px;
	color: #ADD8E6;
}
.create-button{
	width: 80px;
	height: 50px;
	border-radius: 50px;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-shrink: 0;
	font-size: 16px;
	color: #88d4ec;
	box-shadow: -2px 0px 2px 1px rgba(0,0,0,0.1);
}
.create-content:after{
	content: '';
	position: absolute;
	right: 0;
	left: 0;
	bottom: -8px;
	margin: 0 auto;
	height: 20px;
	width: 20px;
	background: #DEEFF5;
	transform: rotate(45deg);
	box-shadow: 1px 1px 5px 2px rgba(0,0,0,0.1);
	z-index: -1;
}
.create-content-box:after{
	content: '';
	position: absolute;
	right: 0;
	left: 0;
	bottom: -8px;
	margin: 0 auto;
	height: 20px;
	width: 20px;
	background: #DEEFF5;
	transform: rotate(45deg);
}
</style>
