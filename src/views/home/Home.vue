<template>
	<div id="home">
		<nav-bar class="home-nav"></nav-bar>
	</div>
</template>

<script>
import NavBar from 'components/common/navbar/Navbar'

import { getHomeMultidata } from 'network/home'

export default {
	name: 'home',
	data() {
		return {
			banners: [],
		}
	},
	components: {
		NavBar,
	},
	created() {
		getHomeMultidata().then((res) => {
			console.log(res)
			this.banners = res.data.banner
		})
	},
}
</script>

<style scoped>
.home-nav {
	background-color: var(--color-tint);
	color: #fff;
}
</style>
