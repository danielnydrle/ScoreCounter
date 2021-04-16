<template>
	<div class="card">
		<h1 :style="scoreStyle">{{score}}</h1>
		<p :style="opponentStyle">{{this.opponentScore}}</p>
		<button @click="handleClick" :style="buttonStyle">&#xFF0B;</button>
	</div>
</template>

<script>
export default {
	name: "Counter",
	data() {
		return {
			score: 0,
			scoreStyle: {
				backgroundImage: `linear-gradient(45deg, ${this.color[0]}, ${this.color[1]})`,
				backgroundSize: "100%",
				backgroundClip: "text",
				textFillColor: "transparent",
			},
			opponentStyle: {
				backgroundImage: `linear-gradient(45deg, ${this.opponentColor[0]}, ${this.opponentColor[1]})`,
				backgroundSize: "100%",
				backgroundClip: "text",
				textFillColor: "transparent",
			},
			buttonStyle: {
				background: `linear-gradient(45deg, ${this.color[0]}, ${this.color[1]})`,
				color: `${this.color[2]}`,
			},
		}
	},
	methods: {
		handleClick() {
			if (this.isDisabled) return; // Button is disabled, halt block execution
			this.$emit("addPoint")
			this.score++;
			this.isDisabled = true;
			
			setTimeout(() => {
				this.isDisabled = false;
			}, 100);
		},
	},
	props: ["color", "opponentScore", "opponentColor"]
}
</script>

<style>
:root {
	--scoreBig: italic normal 700 150px "IBM Plex Mono", monospace;
	--scoreSmall: italic normal 700 100px "IBM Plex Mono", monospace;
	--buttonBig: normal normal 400 100px "IBM Plex Mono", monospace;
	--buttonSmall: normal normal 400 80px "IBM Plex Mono", monospace;
}
.card {
	position: relative;
	text-align: center;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	box-shadow: 0 0 50px 0 rgba(0,0,0,0.5);
	font: var(--scoreBig);
	background: white;
	flex-basis: 35%;
	transition-duration: 0.3s;
	transition-timing-function: ease-in;
	font-variant-numeric: lining-nums;
}
.card:hover {
	transform: scale(1.05);
}
.card h1 {
	font: var(--scoreBig);
	margin: 0;
}
.card p {
	font-size: 30px;
}
.card button {
	border: none;
	width: 100%;
	font: var(--buttonBig);
	display: flex;
	justify-content: center;
	text-align: center;
	padding: 0;
}
@media screen and (max-width: 1024px) {
	.card {
		width: 80%;
	}
	.card h1 {
		font: var(--scoreSmall);
	}
	.card button {
		font: var(--buttonSmall);
	}
}
@media screen and (max-width: 576px) {
	.card {
		width: 100%
	}
}
</style>