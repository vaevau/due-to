<template>
	
	<view class="content">
		<!-- 状态栏 header -->
		<view class="dueto-header" v-if="list.length !==0"> 
		<!-- 状态栏左侧 -->
			<view class="dueto_left">
				<text class="active-text">{{currentTab}}</text>
				<text>{{newData.length}}条</text>
			</view>
			<!-- 状态栏右侧 -->
			<view class="dueto_right">
				<view class="dueto_right-item " :class="{'active-tab': activeIndex === 0}" @click="tab(0)">全部</view>
				<view class="dueto_right-item" :class="{'active-tab': activeIndex === 1}" @click="tab(1)">待办</view>
				<view class="dueto_right-item" :class="{'active-tab': activeIndex === 2}" @click="tab(2)">已完成</view>
			</view>
		</view>
		<!-- 无内容default页面 -->
		<!-- 如果无任何待办事项，header状态栏 不会显示，会显示default页面 -->
		<view class="default"  v-if="list.length ===0"> 
			<view class="default-image">
				<image src="../../static/default.png"></image>
			</view>
			<view class="default-info">
				<view class="default-info_text">您还没有创建任何待办事项,</view>
				<view class="default-info_text">点击下方加号创建</view>
			</view>		
		</view>
		<!-- 主内容区域 -->
		<!-- 如果有待办事项 会显示下面的内容 -->
		<view class="dueto-content" v-else>
			<!-- dueto finished -->
			<view class="dueto-list" :class="{'dueto--finished':item.checked}" v-for="(item,index) in newData" :key="index"
			@click="finish(item.id)">                                                      <!--把list替换成新数据源newData -->
				<view class="dueto-list_checkbox">
					<view class="checkbox"></view>
				</view>
				<view class="dueto-list_content">{{item.content}}</view>
			</view>
		</view>
		<!-- 创建按钮 -->
		<view class="create-dueto" @click="create">
			<text class="iconfont icon-add"></text>
		</view>
		<!-- 输入框 -->
		<view v-if="active" class="create-content">
			<view class="create-content-box">
				<!-- input 输入 -->
				<view class="create-input" >
					<!-- 双向绑定 -->
					<input type="text" v-model="value" placeholder="请输入您要创建的dueto" />
				</view>
				<!-- 发布按钮 -->
				<view class="publish-button" @click="publish">发布</view>	
			</view>
		</view>
	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				value:'', //输入框的值
				list: [],
				active:false, //输入框是否显示开关
				activeIndex: 0 ,//表示当前点击的是谁
				currentTab:' 全部',
			}
		},
		onLoad() {

		},
		computed: {     //动态监听数据变化
			newData(){  //定义一个新数据源
				let list = JSON.parse(JSON.stringify(this.list)) //获取源数据
				let newList = [] //新建一个空数组用来存放需要处理后的数据
				if(this.activeIndex === 0){ //点击全部tab
					this.currentTab = '全部' // header左侧当前标签
					return list 
				}
				if(this.activeIndex === 1){ //点击待办tab
					　//check 为false 时
					list.forEach((item)=>{
						if(!item.checked){
							newList.push(item)
						}
					})
					this.currentTab = '待办'
					return newList
				}
				if(this.activeIndex === 2){ //点击已完成tab
				//check 为true 时
					list.forEach((item)=>{
						if(item.checked){
							newList.push(item)
						}
					})
					this.currentTab = '已完成'
					return newList
				}
			
			},
		},
		methods: {
			//点击创建按钮弹出输入框
			create() {
				this.active = true
			},
			//发布内容
			publish(){
				if(this.value === ''){  //禁止发布空内容
					uni.showToast({
						title:"请输入内容", //当输入空白内容时提示信息
						icon:'none'  //不限时提示图标
					})
					return  //返回阻止添加空内容待办事项
				}
				this.list.unshift(
				{
					id:'id'+ new Date().getTime(), //获取唯一id（时间戳）
					content:this.value,//待办事项为输入框的值
					checked:false //待办事件是否完成开关
				})
				this.value = ''   //清空input 
				this.active = false // 收起输入框
			},
			// 完成状态
			finish(id){
				// let index = this.list.findIndex(item => item.id === id) 箭头函数写法
				let index = this.list.findIndex(function(item){ return item.id === id })
				console.log('我被点击了', this.list[index])
				this.list[index].checked = !this.list[index].checked //切换是否完成
			},
			tab(index){
				this.activeIndex = index //那个tab需要高亮
			}
		
		}
	}
</script>

<style>
	@import "../../common/icon.css";
.dueto-header{
	cursor: pointer;
	display: flex;
	align-items: center;
	font-size: 14px;
	font-family: Arial, Helvetica, sans-serif;
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
	font-size: 14px;
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
	cursor: pointer;
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
	font-size: 14px;
}
.publish-button{
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
	cursor: pointer;
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

	
.default{
	padding-top: 70px;
}
.default-image{
	display: flex;
	justify-content: center;
}

.default-info{
	text-align: center;
}
.default-info_text{
	font-size: 14px;
	color: #C0C0C0;
}
</style>
