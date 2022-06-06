<template>
	<v-container class="container">
		<v-row>
			<v-col>
				<v-btn
					elevation="2"
				>
					サンプルボタン
				</v-btn>
			</v-col>
		</v-row>

		<v-row class="row">
			<v-col
				cols="12" sm="6" md="3" lg="1"
				v-for="n in 50"
				:key="n"
			>
				<v-card class="card">
					<v-img
						aspect-ratio="2"
						contain
						height="50px"
						width="100px"
						src="../assets/dio.jpg"
					>
					</v-img>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>

</script>

<style>

.row {
	text-align: center;
}
.card {
	margin: 0 auto;
}


</style>
