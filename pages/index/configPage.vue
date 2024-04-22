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
	<br><br>
	<view class="main">
		<br>
		<view class="myInfo">
			<up-avatar :src="src" shape="circle" size=90></up-avatar>
			<view class="myTell">
				<text >
					Hi,我是菠菜
				</text>
				<br>
				<text>
					欢迎光临我的app
				</text>
				<br>
				<text>
					同时希望关注我的菠菜呜!
				</text>
				<br>
				<text>
					不慌不忙，祝你一切顺利🍃
				</text>
			</view>
		</view>
		<br>
		<view class="cell">
			<up-cell-group>
				<up-cell icon="grid-fill" title="权限检查" isLink url="pages/index/callPermissions"></up-cell>
				<up-cell icon="gift" title="为菠菜捐款" value="您的大恩大德此生难忘" isLink url="pages/index/gift"></up-cell>
				<up-cell icon="heart" title="特别鸣谢" label="(感谢c的审美方针)" value="@soladuor"></up-cell>
			</up-cell-group>
		</view>

	</view>
</template>

<script setup>
	const src="http://47.238.163.138:9111/api/v1/buckets/phone-call/objects/download?preview=true&prefix=dHh6c2IucG5n&version_id=null"
</script>

<style scoped>
	.main{
		display: flex;
		height: 100vh;
		width: 100%;
		background-color: beige;
		flex-flow: column;
	}
	.myInfo{
		margin-top: 2rem;
		margin-left: 2rem;
		display: flex;
		flex-direction: row;
	}
	.cell{
		display: flex;
		height: auto;
		width: 100%;
	}
	.u-nav-slot{
		display: flex;
		flex-direction: row;
	}
	.myTell{
		color: #f9ae3d;
		padding-left: 1.5rem;
		font-style: oblique;
		/* font-weight: bold; */
	}
</style>
