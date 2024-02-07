<template>
	<FormSide />
</template>

<script>
import FormSide from './components/FormSide.vue';

export default {
	methods: {},
	name: 'App',
	components: {
		FormSide
	}
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500&display=swap');
#app {
	font-family: 'Space Grotesk', sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	overflow: hidden;
	color: hsl(278, 68%, 11%);
	height: 100vh;
	width: 100vw;
}
</style>
