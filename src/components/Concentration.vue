<template>
	<div>
		<h1>Concentration</h1>
		<v-btn
			elevation="2"
			@click="gameStart"
		>
		ゲームを始める
		</v-btn>

		<!--
		トランプのレイアウト
		-->
		<v-row
			class="blue lighten-4"
			style="height: 450px;"
			justify="center"
			align-content="center"
		>
			<v-col
				cols=3
				v-for="item in items"
				:key="item"
			>
				<v-card
					class="d-flex pa-2"
					elevation="6"
					color="purple"
					outlined
					shaped
					height=150
					max-width="200"
					@click="choiceCards(item.name)"
				>
					<v-list-item three-line>
						<v-img
							height="50px"
							width="100px"
							src="../assets/JoJo's_Bizarre_Adventure_logo.png"
						>
						</v-img>
						<v-list-item-title>
							{{ item.name }}
						</v-list-item-title>
					</v-list-item>
				</v-card>
			</v-col>
		</v-row>
		<v-card-title>
			カードを選んでください。残り {{ cards_count }} 枚
		</v-card-title>
	</div>
</template>

<script>
export default {
	name: 'Concentration-Game',
	data: function() {
		return {
			items: [
				{name: "ポルナレフ"},
				{name: "ジョジョ"},
				{name: "花京院典明"},
				{name: "DIO"},
				{name: "ポルナレフ"},
				{name: "ジョジョ"},
				{name: "花京院典明"},
				{name: "DIO"},
			],
			cards: [],
			cards_count: 2,
		}
	},
	methods: {
		// カード選択
		choiceCards: function(name) {
			this.cards.push(name);
			this.cards_count--;
			// if (this.cards_count == 0) {
			// 	alert("この2枚のカードで良いですか？")
			// }
			if (this.cards_count == 0) {
				this.judge_card(this.cards);
				this.set_flg();
			}
		},
		// ゲーム開始
		gameStart: function() {
			alert("貴様・・みているな！！ゲーム開始！")
		},
		// カードが一致しているかジャッジする
		judge_card: function(cards) {
			if (cards[0] == cards[1]) {
				alert("正解！")
			} else {
				alert("ブブー！")
			}
		},
		set_flg: function() {
			this.cards_count = 2;
			this.cards = [];
		}
	}

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
	margin: 40px 0 0;
}
ul {
	list-style-type: none;
	padding: 0;
}
li {
	display: inline-block;
	margin: 0 10px;
}
a {
	color: #42b983;
}
</style>
