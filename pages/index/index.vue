<template>
	<view class="main">
		<view class="content">
			<view class="phone">
				<text>请输入电话号码:</text>
				<up-input 
					placeholder="号码为..." 
					prefixIcon="phone" 
					prefixIconStyle="font-size: 22px;color: #909399"
					v-model="phoneNumber">
				</up-input>
			</view>
			<br>
			<view class="config">
				<view class="configContent">
					<br>
					<!-- 循环次数 -->
					<view class="changeNumber">
						<text>循环次数:</text>
						&nbsp;&nbsp;&nbsp;
						&nbsp;&nbsp;&nbsp;
						&nbsp;&nbsp;&nbsp;
						&nbsp;&nbsp;&nbsp;
						<up-number-box v-model="cycleNumberValue" >
						</up-number-box>
					</view>
					<br>
					<!-- 循环间隔 -->
					<view class="cycleIntervals">
						<text>循环拨打间隔(s):</text>
						&nbsp;
						<up-number-box v-model="cycleIntervalsValue" >
						</up-number-box>
					</view>
					<br>
				</view>
			</view>
			<br>
			<view class="buttonContent">
				<view class="callButton">
					<up-button 
						type="warning" 
						:plain="true" 
						text="call" 
						size="large"
						icon="warning"
						@click="startCalling">
						</up-button>
				</view>
				&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
				<view class="callButton">
					<up-button 
						type="success" 
						:plain="true" 
						text="中断" 
						size="large"
						icon="pause-circle"
						@click="stopChange">
						</up-button>
				</view>
			</view>
			
			<view class="warningText">
				<up-text type="warning" text="
				
				并不会在通话结束后再开启下一次循环,
				而是会根据设定的间隔时间进行每次循环;
				若对方长期不接电话:
				建议将循环间隔拉长后挂机以确保最佳效果"
				/>
			</view>
			
			<view class="check">
				<up-text type="error" text="不生效?点击这里" @click="goToCheck" />
			</view>
		</view>
	</view>
</template>

<script setup>
	import { ref } from 'vue';
	const phoneNumber=ref('') 
	const cycleNumberValue=ref(1)
	const cycleIntervalsValue=ref(1)
	const stop=ref(false)
	async function startCalling(){
		console.log("调用了startCalling")
		/* 先获取手机号的值,再传给call方法 */
		console.log("手机号="+phoneNumber.value)
		for(let i=0;i<cycleNumberValue.value;i++){
			if(stop.value!=true){
				await call(phoneNumber.value);
				await delay(cycleIntervalsValue.value)
				console.log(`循环次数${cycleNumberValue.value}`)
				console.log(`循环间隔${cycleIntervalsValue.value}`)
				console.log(`第${i}次循环`)
			}else{
				break
			}
		}
		/* 纠结一下 */
		stop.value=false
	}
	function call(phoneNumber){
		console.log("调用了call")
		//导入Activity、Intent类
		var Intent = plus.android.importClass("android.content.Intent")
		var Uri = plus.android.importClass("android.net.Uri")
		//获取主Activity对象实例
		var main = plus.android.runtimeMainActivity()
		//创建Intent
		var uri= Uri.parse("tel:"+phoneNumber)
		var call=new Intent("android.intent.action.CALL",uri)
		//调用startActivity方法拨打电话
		main.startActivity(call)
		console.log("ok")
	}
	function delay(ms) {
		return new Promise(resolve => setTimeout(resolve, ms*1000));
	}
	function stopChange(){
		stop.value=true
	}
	//权限检查
	function goToCheck(){
		console.log("点击跳转方法")
		uni.navigateTo({
			url: '/pages/index/configPage'
		})
	}
</script>

<style scoped>
 .main{
	display: flex;
	height: 100vh;
	width: 100%;
	background-color: beige;
	align-items: center;
	justify-content: center;
 }
 .content{
	 display: flex;
	 height: auto;
	 width: auto;
	 align-items: center;
	 justify-content: center;
	/* line-height: 50%; */
	flex-flow: column; /* 子组件纵向布局 */
 }
 .phone{
	 height: auto;
	 width: auto;
	 background-color: paleturquoise;
	 border-radius: 25px;
	 text-align: center;
	 padding-top: 7px;
 }
 .config{
	 display: flex;
	 height: auto;
	 width: 300px; /* 300px*/
	 align-items: center;
	 justify-content: center;
	/* line-height: 50%; */
	flex-flow: column; /* 子组件纵向布局(需设为弹性盒子) */
	background-color: paleturquoise;
	border-radius: 25px;
 }
 .configContent{
	 text-align: center;
 }
 .changeNumber{
	 display: flex;
	 flex-direction: row; /* 子组件横向布局(需设为弹性盒子) */
 }
 .cycleIntervals{
	 display: flex;
	 flex-direction: row;
 }
 .buttonContent{
	 display: flex;
	 flex-direction: row;
 }
text{
	font-weight: bold;
	color: forestgreen;
}
</style>
