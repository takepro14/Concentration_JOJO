<template>
	<div id="app">
		<Concentration />
	</div>
</template>

<script>
import Concentration from './components/Concentration.vue'

export default {
	name: 'App',
	components: {
		Concentration
	}
}
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
