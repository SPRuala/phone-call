<template>
	<view class="navbar">
		<up-navbar
			:auto-back="true"
		    :safeAreaInsetTop="true"
			bgColor="#f5f5dc"
			:border="false"
		>
			<template #left>
				<view class="u-nav-slot">
					<up-icon name="arrow-leftward" size="25"/>
					<up-text text="返回" size="20" style="margin-left: 1rem;"/>
				</view>
			</template>
		</up-navbar>
	</view>
	<view class="main">
		<view class="checkPermission">
			您的电话权限为：
			{{callPermissionStatus}}
		</view>
		<view class="tip">
			<up-text type="warning" text="
			若显示未授权,
			请在手机设置页面检查是否给予电话权限"
			 />
		</view>
	</view>
</template>

<script setup>
import { ref } from 'vue';
	let callPermissionStatus=ref('未授权')
	plus.android.requestPermissions(["android.permission.CALL_PHONE"], (resultObj) => {
		console.log(resultObj)
		var result;
		var grantedPermission = resultObj.granted[0];
		console.log('已获取的权限：' + grantedPermission);
		callPermissionStatus.value = "已授权"
	})
</script>

<style scoped>
	.main {
		display: flex;
		height: 100vh;
		width: 100%;
		background-color: beige;
		align-items: center;
		justify-content: center;
		flex-flow: column;
	}
	.u-nav-slot{
			display: flex;
			flex-direction: row;
	}
</style>