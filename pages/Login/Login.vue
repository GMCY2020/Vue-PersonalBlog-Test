<template>
	<view class="Login">
		<view>登录</view>
		<view class="item">
			<input class="user" type="text" placeholder="账号" v-model="this.user">
			<input class="password" type="text" placeholder="密码" v-model="this.password" password>
		</view>
		<button class="btn" @click="this.Login()">登录</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				user: "",
				password: ""
			};
		},

		methods: {
			Login() {

				if (this.user === "demo" && this.password == "123") {

					console.log(this.user)
					console.log(this.password)

					uni.showToast({
						title: '登录成功',
						duration: 2000,
						icon: 'none'
					});

					uni.navigateTo({
						url: "/pages/index/index"
					})

				} else {
					uni.showToast({
						title: '登录失败',
						duration: 2000,
						icon: 'none'
					});
				}
			}
		}
	}
</script>

<style lang="scss">
	body,
	html,
	page {
		height: 100%;
		width: 100%;
		margin: 0 auto;

		background-color: #3f4654;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.Login {
		background-color: #ffffff;

		width: 400px;
		height: 300px;

		border-radius: 12.5px;

		padding: 25px;

		display: flex;
		flex-direction: column;

		justify-content: space-between;

		align-items: center;

		font-size: 25px;

		box-shadow: 0 1px 6px 0 #cccccc;


		.item {}

		.user,
		.password {
			background-color: #eeeeee;
			margin: 12.5px;
			padding: 7.5px;
			width: 350px;
			height: 35px;

			font-size: 25px;

			border-radius: 12.5px;
		}

		.btn {
			width: 350px;
			background-color: #cccccc;
		}
	}
</style>