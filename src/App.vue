<template>
	<div class="container">
		<div class="current-time">{{ formattedTime }}</div>

		<h1 class="main-title">Welcome to Kimoiran's Website</h1>
		<el-row :gutter="20" justify="center">
			<el-col
				:xs="24"
				:sm="12"
				:md="8"
				:lg="6"
				:xl="4"
				v-for="(link, index) in links"
				:key="index"
				style="margin-bottom: 10px"
			>
				<a :href="link.url" class="nav-link" target="_blank">{{ link.text }}</a>
			</el-col>
		</el-row>
	</div>
</template>

<script>
export default {
	data() {
		return {
			searchQuery: "",
			currentTime: new Date(),
			timeInterval: null,
			links: [
				{ text: "常用软件下载", url: "https://webnavigate.github.io/Software" },
				{ text: "上网登录窗", url: "http://192.168.7.221/" },
				{ text: "长沙理工大学", url: "https://www.csust.edu.cn/" },
				{ text: "起点中文网", url: "https://www.qidian.com/all/" },
				{ text: "ViLiPix", url: "https://www.vilipix.com/" },
				{ text: "BiLiBiLi", url: "https://bilibili.com/" },
				{ text: "通义千问", url: "https://tongyi.aliyun.com/qianwen/" },
				{ text: "DeepSeek", url: "https://chat.deepseek.com/" },
			],
		};
	},
	computed: {
		formattedTime() {
			const options = {
				weekday: "long",
				year: "numeric",
				month: "long",
				day: "numeric",
				hour: "2-digit",
				minute: "2-digit",
				second: "2-digit",
				hour12: false,
			};
			return new Intl.DateTimeFormat("zh-CN", options).format(this.currentTime);
		},
	},
	mounted() {
		this.timeInterval = setInterval(() => {
			this.currentTime = new Date();
		}, 1000);
	},
	beforeUnmount() {
		clearInterval(this.timeInterval);
	},
	methods: {
		handleSearch() {
			if (this.searchQuery.trim()) {
				window.location.href = `https://www.bing.com/search?q=${encodeURIComponent(
					this.searchQuery
				)}`;
			}
		},
	},
};
</script>

<style>
body {
	background-image: url("./assets/24.jpg");
	background-size: cover;
	background-position: center;
	min-height: 100vh;
	margin: 0;
	font-family: Arial, sans-serif;
}

.container {
	max-width: 1200px;
	margin: 0 auto;
	padding: 20px;
}

.current-time {
	color: white;
	text-align: center;
	margin-bottom: 20px;
}

.main-title {
	color: #ff00ff;
	text-align: center;
	margin: 30px 0;
}

.nav-link {
	display: block;
	text-align: center;
	padding: 15px;
	color: #bbffff;
	background-color: rgba(0, 0, 0, 0.5); /* 提高可读性 */
	border-radius: 5px;
	text-decoration: none;
	transition: all 0.3s ease;
}

.nav-link:hover {
	color: #ff6600;
	transform: translateY(-2px);
}
</style>