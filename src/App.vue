<template>
	<v-app>
		<v-navigation-drawer app>
			<!-- -->
		</v-navigation-drawer>

		<v-app-bar app>
			<!-- -->
		</v-app-bar>

		<!-- アプリケーションのコンポーネントに基づいてコンテンツのサイズを決定 -->
		<v-main>

			<!-- アプリケーションに適切なgutterを提供 -->
			<v-container fluid>

			<!-- vue-routerを使用する場合 -->
			<router-view></router-view>

			<Concentration />
			<!--
			<Vdialog />
			<GridDegign />
			-->
			</v-container>
		</v-main>
		<v-footer app>
			<!-- -->
		</v-footer>
	</v-app>
</template>

<script>
import Concentration from './components/Concentration';
// import GridDegign from './components/GridDegign';
// import Vdialog from './components/Vdialog.vue';

export default {
	name: 'App',

	components: {
		Concentration,
		// GridDegign
		// Vdialog
	},

	data: () => ({
		//
	}),
};
</script>
