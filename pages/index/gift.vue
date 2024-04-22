<template>
	<view class="main">
		<view class="thanksText">
			<up-text type="warning" text="蟹蟹您的捐献!" size="30"></up-text>
		</view>
		<up-switch v-model="payFunction"></up-switch>
		<text class="tip">{{payFunction===false?'支付宝':'没有微信二维码哈哈'}}</text>
		<br>
		<view class="twohorseZFB">
			<up-qrcode :size="200" val="谢谢您的心意!很高兴受到您的喜欢!(不会收钱滴)" background="#f5f5dc" foreground="#afeeee" showLoading loading-text="耶~~"></up-qrcode>
		</view>
		<br>
		<view class="endText">
			<up-text type="warning" text="蟹蟹您的好心！紫色南瓜" size="15"></up-text>
			<text style="padding-left: 80px;">—菠菜 {{nowDay}}</text><br>
			<text style="padding-left: 150px;">{{nowTime}}</text>
		</view>
	</view>
</template>

<script setup>
	import { ref } from 'vue';
	var time = new Date()
	var year = time.getFullYear()
	var month = time.getMonth()+1
	var day = time.getDate()
	var hour=time.getHours()
	var min=time.getMinutes()
	var second=time.getSeconds()
	let nowDay=ref(year+'-'+(month<10?'0'+month:month)+'-'+(day<10?'0'+day:day))
	let nowTime=ref((hour<10?'0'+hour:hour)+':'+(min<10?'0'+min:min)+':'+(second<10?'0'+second:second))
	const payFunction=ref(false)
</script>

<style>
.main{
	display: flex;
	height: 100vh;
	width: 100%;
	background-color: beige;
	align-items: center;
	justify-content: center;
	flex-flow: column;
}
.endText{
	padding-left: 130px;
}
text{
	color: #f9ae3d;
	padding-left: 3rem;
}

/* .twohorseZFB{
	display: none;
} */
</style>
