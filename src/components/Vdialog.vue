<template>
	<div class="text-center">
		<v-dialog
			v-model="dialog"
			width="500"
		>
			<!-- ボタン -->
			<template v-slot:activator="{ on, attrs }">
				<v-btn
					color="red lighten-2"
					dark
					v-bind="attrs"
					v-on="on"
					v-for="(item, index) in items"
					:key="index"
					@click="getName(item.name)"
				>
					{{ index }}: {{ item.name }} - {{ item.sugar }}
				</v-btn>
			</template>

			<!-- ダイアログ -->
			<v-card>
				<v-card-title
					class="headline grey lighten-2"
					primary-title
				>
					{{ selected }}
				</v-card-title>

				<v-card-text>
					Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
				</v-card-text>

				<v-divider></v-divider>

				<v-card-actions>
					<v-spacer></v-spacer>
					<!-- ボタン(押すとダイアログを閉じる) -->
					<v-btn
						color="primary"
						text
						@click="dialog = false"
					>
						I accept
					</v-btn>
				</v-card-actions>
			</v-card>

		</v-dialog>
	</div>
</template>

<script>
export default {
	name: 'Vdialog-test',
	data() {
		return {
			// デフォルトはfalse状態
			dialog: false,
			items: [
				{name: 'りんご', sugar: 10},
				{name: 'ぶどう', sugar: 5},
				{name: 'めろん', sugar: 15}
			],
			selected: ""
		}
	},
	methods:  {
		getName: function(name) {
			this.selected = name;
		}
	}
}
</script>
