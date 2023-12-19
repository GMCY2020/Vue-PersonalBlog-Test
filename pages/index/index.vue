<template>
	<!-- 文章，图片，项目展示界面 -->
	<view class="contain">
		<view class="top">
			<view class="top-title">
				个人博客
			</view>
			<image class="top-img-head" src="../../static/top-img.png" @mousemove="this.open()" mode="heightFix">
			</image>
		</view>

		<view class="login-message" v-if="this.showLoginMessage" @mousemove="this.open()" @mouseout="this.close()">
			<view class="login-message-home" @click="this.home()">
				首页
			</view>
			<view class="login-message-out" @click="this.outLogin()">
				退出登录
			</view>
		</view>


		<view class="mid" @mousemove="this.close()">
			<view class="left">

				<view class="left-item" id="person">
					<image class="img-head" src="../../static/top-img.png" mode="widthFix"></image>

					<view class="username">
						用户名
					</view>

					<view class="individual-label">
						签名
					</view>

					<view class="messages">
						<view class="messages-item">
							<view class="messages-item-number">
								3
							</view>
							<view class="messages-item-til">
								项目
							</view>
						</view>
						<view class="messages-item">
							<view class="messages-item-number">
								1
							</view>
							<view class="messages-item-til">
								文章
							</view>
						</view>
						<view class="messages-item">
							<view class="messages-item-number">
								2
							</view>
							<view class="messages-item-til">
								相册
							</view>
						</view>
					</view>

				</view>

				<view class="left-item" id="pan">
					<view class="title">
						项目
					</view>

					<view class="line" />

					<view class="detail" @click="this.goTo('project', 1)">
						<view class="choice" v-if="this.type === 'project' && this.id === '1'">
							{{this.projects[0][0]}}
						</view>
						<view class="choice-no" v-else>
							{{this.projects[0][0]}}
						</view>
					</view>

					<view class="detail" @click="this.goTo('project', 2)">
						<view class="choice" v-if="this.type === 'project' && this.id === '2'">
							{{this.projects[1][0]}}
						</view>
						<view class="choice-no" v-else>
							{{this.projects[1][0]}}
						</view>
					</view>
					<view class="detail" @click="this.goTo('project', 3)">
						<view class="choice" v-if="this.type === 'project' && this.id === '3'">
							{{this.projects[2][0]}}
						</view>
						<view class="choice-no" v-else>
							{{this.projects[2][0]}}
						</view>
					</view>
				</view>

				<view class="left-item" id="pan">
					<view class="title">
						文章
					</view>

					<view class="line" />

					<view class="detail" @click="this.goTo('article', 1)">
						<view class="choice" v-if="this.type === 'article' && this.id === '1'">
							MarkDown使用
						</view>
						<view class="choice-no" v-else>
							MarkDown使用
						</view>

					</view>
				</view>


				<view class="left-item" id="pan">
					<view class="title">
						相册
					</view>

					<view class="line" />

					<view class="detail" @click="this.goTo('photo', 1)">
						<view class="choice" v-if="this.type === 'photo' && this.id === '1'">
							{{this.photos[0][0]}}
						</view>
						<view class="choice-no" v-else>
							{{this.photos[0][0]}}
						</view>
					</view>

					<view class="detail" @click="this.goTo('photo', 2)">
						<view class="choice" v-if="this.type === 'photo' && this.id === '2'">
							{{this.photos[1][0]}}
						</view>
						<view class="choice-no" v-else>
							{{this.photos[1][0]}}
						</view>
					</view>
				</view>


			</view>

			<view class="right">

				<view class="right-item" id="project" v-if="this.type === 'project'">
					<view class="title">
						{{this.projects[this.id-1][0]}}
					</view>
					<view class="bilbil">
						<iframe class="bilbil-video" :src="this.projects[this.id-1][1]" scrolling="no" border="0"
							frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
					</view>

					<view class="messages">
						<view class="messages-detail">
							项目地址
						</view>
						<uni-link class="messages-detail" :href="this.projects[this.id-1][2]" text="Gitee"></uni-link>
					</view>

				</view>


				<!-- 文章 -->
				<view class="right-item" id="article" v-if="this.type === 'article'">
					<zero-markdown-view :markdown="this.articles[this.id - 1]"></zero-markdown-view>
				</view>


				<!-- 图片 -->
				<view class="right-item" id="photo" v-if="this.type === 'photo'">
					<view class="title-box">
						<view class="title">
							{{this.photos[this.id - 1][0]}}
						</view>
					</view>

					<view class="img-boxs">

						<uni-swiper-dot :info="this.info" :current="this.current" field="content" :mode="this.mode">
							<swiper class="swiper-box" @change="change">
								<swiper-item v-for="(item ,index) in this.photos2[this.id-1]">
									<view class="swiper-item">
										<image class="img-item" :src="'../../static/photos/' + item[1]" mode="widthFix">
										</image>
									</view>
								</swiper-item>
							</swiper>
						</uni-swiper-dot>

						<block v-for="(item, index) in this.photos[this.id - 1]">
							<view class="img-box" v-if="index !== 0">
								<view class="title">
									{{item[0]}}
								</view>
								<image class="img-item-2" :src="'../../static/photos/' + item[1]" mode="widthFix">
								</image>
							</view>
						</block>
					</view>

				</view>

				<view class="right-item" id="home"
					v-if="this.type !== 'photo' && this.type !== 'article' && this.type !== 'project'">
					<image class="home-img" src="../../static/photos/earth.jpg" mode="heightFix"></image>
				</view>

			</view>
		</view>

		<view style="height: 10rpx;" />
	</view>

</template>

<script>
	export default {
		data() {
			return {
				url: "../../static/MarkDown语言技巧.md",
				markdownDatas: "",
				showLoginMessage: false,

				type: null,
				id: null,

				projects: [
					["测试B站地址1",
						"https://player.bilibili.com/player.html?aid=356764465&bvid=BV17X4y1a7Fh&cid=1148975564&page=1",
						"https://gitee.com/explore"
					],
					["测试B站地址2",
						"https://player.bilibili.com/player.html?aid=784285239&bvid=BV1W24y1P7ZS&cid=1148366968&page=1",
						"https://gitee.com/explore"
					],
					["测试B站地址3",
						"https://player.bilibili.com/player.html?aid=271668186&bvid=BV1ac411G7vc&cid=1147467778&page=1",
						"https://gitee.com/explore"
					]
				],

				articles: [
					"# 文章(Md文件)\n ### 表格\n | 表头 | 表头 | 表头 | 表头 |\n | :--: | :--: | :--: | :--: |\n | 单元格 | 单元格 | 单元格 | 单元格 |\n | 单元格 | 单元格 | 单元格 | 单元格 |\n ### 代码\n ```python\n int a = 1\n ```\n ### 表格\n | 表头 | 表头 | 表头 | 表头 |\n | :--: | :--: | :--: | :--: |\n | 单元格 | 单元格 | 单元格 | 单元格 |\n | 单元格 | 单元格 | 单元格 | 单元格 |\n ### 代码\n ```python\n int a = 1\n ```\n  ### 表格\n | 表头 | 表头 | 表头 | 表头 |\n | :--: | :--: | :--: | :--: |\n | 单元格 | 单元格 | 单元格 | 单元格 |\n | 单元格 | 单元格 | 单元格 | 单元格 |\n ### 代码\n ```python\n int a = 1\n ```\n",
				],

				info: [{
					content: '内容 A'
				}, {
					content: '内容 B'
				}, {
					content: '内容 C'
				}],

				current: 0,

				mode: 'round',

				photos: [
					[
						"相册1",
						["图-1", "图-1.png"],
						["图-2", "图-2.png"],
						["图-3", "图-3.png"]
					],
					[
						"相册2",
						["图-4", "图-4.png"],
						["图-5", "图-5.png"],
					]
				],
				photos2: [
					[
						["图-1", "图-1.png"],
						["图-2", "图-2.png"],
						["图-3", "图-3.png"]
					],
					[
						["图-4", "图-4.png"],
						["图-5", "图-5.png"],
					]
				],
			}
		},

		onLoad(options) {
			this.type = options.type
			this.id = options.id
		},

		methods: {
			open() {
				this.showLoginMessage = true
			},

			close() {
				this.showLoginMessage = false
			},

			change(e) {
				this.current = e.detail.current;
			},

			outLogin() {
				uni.navigateTo({
					url: "/pages/Login/Login"
				})
			},

			goTo(type, id) {
				uni.navigateTo({
					url: '/pages/index/index?type=' + type + "&id=" + id
				})

			},

			home() {
				uni.navigateTo({
					url: '/pages/index/index'
				})
			},
		},
	}
</script>





<style lang="scss">
	body,
	html,
	page {
		background-color: #3f4654;
		width: 100%;
		min-width: 1000px;
		margin: 0 auto;

		overflow-x: auto;
	}

	.top {
		position: fixed;
		min-width: 100%;
		width: max-content;
		top: 0px;
		left: 0px;
		z-index: 999;

		background-color: #21242d;
		height: 60px;

		display: flex;
		justify-content: space-between;
		align-items: center;

		color: #f9fbfb;

		.top-title {
			padding: 3px;
			margin: 4px;
			margin-left: 40px;
		}

		.top-img-head {
			border-radius: 50%;
			margin-right: 40px;
			height: 65%;
			border: 1px solid #3f4654;
		}
	}

	.login-message {
		background-color: #21252b;

		position: fixed;
		top: 61px;
		right: 10px;
		z-index: 999;

		border-radius: 3px;

		color: #ffffff;

		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;

		.login-message-home,
		.login-message-out,
		.login-message-Login {
			padding: 12.5px;
		}

		.login-message-home,
		.login-message-Login {
			padding-left: 30px;
			padding-right: 30px;
		}

	}

	.mid {
		margin-top: 60px;

		display: flex;

		.left {
			width: 20%;
			margin-left: 25px;
			margin-top: 20px;


		}

		.right {
			width: 80%;
			margin-right: 25px;
			margin-top: 20px;
		}

		.left-item,
		.right-item {
			margin: 5px;
			margin-bottom: 10px;
			background-color: #ffffff;
			border-radius: 7.5px;


		}

		.right-item {}
	}



	.img-boxs {
		.title {
			font-size: 30px;
		}

		.img-box {
			width: 100%;
			display: flex;
			flex-direction: column;
			align-items: center;

			margin-bottom: 40px;

			.img-item-2 {
				width: 96%;
				margin: 15px;
				border-radius: 10px;
			}
		}
	}

	#photo {
		.title-box {
			display: flex;
			flex-direction: column;
			align-items: center;
			font-size: 50px;
			font-weight: bold;

			.title {
				padding: 25px;
			}
		}

		.swiper-box {
			height: 500px;

			padding: 25px;

			.swiper-item {

				.img-item {
					width: 100%;
				}
			}
		}
	}

	#project {
		.title {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			font-weight: bold;
			font-size: 25px;
			padding: 25px;
		}

		.bilbil {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;




			.bilbil-video {
				height: 645px;
				width: 98%;
				border-radius: 15px;
			}
		}

		.messages {
			display: flex;

			.messages-detail {
				padding: 15px;
			}
		}
	}

	.bottom {
		height: 250px;
		margin: 25px;
		background-color: #21242d;
		border-radius: 7.5px;
	}

	#person {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: auto;

		.img-head {
			border-radius: 50%;
			border: 5px solid #ffffff;
			width: 120px;

			position: relative;
			top: -10px;
		}

		.username {
			font-weight: bold;
			font-size: 25px;
		}

		.individual-label {
			margin: 12.5px;
			color: #ababab;
		}

		.messages {
			display: flex;

			.messages-item {
				padding: 17.5px;
				display: flex;
				flex-direction: column;
				justify-content: center;
				align-items: center;

				color: #005980;

				.messages-item-number {
					font-size: 20px;
				}

				.messages-item-til {
					font-size: 12.5px;
				}
			}
		}
	}

	#pan {
		.title {
			padding: 12.5px;
			padding-bottom: 5px;
		}

		.detail,
		.more {}

		.more {
			text-align: center;
		}

		.choice {
			background-color: #cccccc;
			border-radius: 10px;
			padding: 12.5px;
		}

		.choice-no {
			padding: 12.5px;
		}


	}

	#home {
		width: 100%;
		height: 98%;
		display: flex;
		justify-content: center;

		background-color: rgba(1, 1, 1, 0);

		.home-img {
			height: 100%;
			border-radius: 25px;
		}
	}

	.line::after {
		content: '';
		width: 99%;
		height: 1px;
		display: block;
		margin: 0 auto;
		border-bottom: 2px solid #ababab;
		padding: 1px;
	}
</style>