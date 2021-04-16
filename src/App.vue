<template>
	<v-app>
		<Counter id="counterOne" :color="colorOne" @addPoint="scoreOne++" :opponentScore="scoreTwo" :opponentColor="colorTwo" />
		<Counter id="counterTwo" :color="colorTwo" @addPoint="scoreTwo++" :opponentScore="scoreOne" :opponentColor="colorOne" />
	</v-app>
</template>

<script>
import Counter from "./components/Counter.vue"


const colors = [
	["#00b894", "#81ecec", "white"],
	["#ff7675", "#d63031", "white"],
	["#273c75", "#192a56", "white"],
	["#353b48", "#2f3640", "white"],
	["#7f8fa6", "#718093", "black"],
	["#ff9ff3", "#f368e0", "black"],
	["#5f27cd", "#341f97", "white"],
	["#b33771", "#6d214f", "white"],
	["#ed4c67", "#6f1e51", "white"],
	["#dfe6e9", "#2d3436", "black"]
]

export default {
	name: 'App',
	components: {
		Counter
	},
	data() {
		return {
			colorOne: colors[Math.floor(Math.random() * colors.length)],
			colorTwo: colors[Math.floor(Math.random() * colors.length)],
			scoreOne: 0,
			scoreTwo: 0,
		}
	},
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:ital,wght@0,400;1,700&display=swap');

html, body, v-app {
	height: 100vh;
	width: 100vw;
	margin: 0;
	padding: 0;
	background-color: white;
}
v-app {
	display: flex;
	justify-content: space-evenly;
	align-items: center;
}
@media screen and (max-width: 1366px) {
	#counterTwo {
		transform: rotate(180deg);
	}
}
@media screen and (max-width: 1024px) and (orientation: portrait) {
	v-app {
		flex-direction: column;
		justify-content: space-around;
	}
	#counterOne {
		transform: rotate(180deg);
	}
	#counterTwo {
		transform: rotate(0);
	}
}
@media screen and (max-width: 576px) {
}
</style>
