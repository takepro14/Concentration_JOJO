<template>
	<v-container>
		<v-row>
			<h1>
				JOJO's Bizzare Concentration
			</h1>

			<v-col>
				<ul>
					<v-alert
						v-show="getFlg"
						border="bottom"
						color="pink darken-1"
						dark
					>
						<li>承太郎「おいジジイ、そりゃあ {{ card }} のカードだぞ」</li>
					</v-alert>
				</ul>
			</v-col>

		</v-row>
		<v-row>
			<v-col cols="2">
				<v-btn
					elevation="2"
					@click="gameStart"
				>
					ゲームを始めるゥゥ！！
				</v-btn>
			</v-col>
			<v-col>
				<v-card-title>
					カードを選んでください。残り {{ cards_count }} 枚
				</v-card-title>
			</v-col>
		</v-row>

		<!--
		トランプのレイアウト
		-->
		<v-row
			style="height: 450px"
			justify="center"
			align-content="center"
		>
			<v-col
				cols="12" sm="6" md="4" lg="3"
				v-for="item in items"
				:key="item"
			>
				<v-card
					class="d-inline-flex pa-2"
					elevation="2"
					color="deep-purple lighten-3"
					outlined
					shaped
					height=100
					max-width="200"
					@click="choiceCards(item)"
				>
					<v-list-item three-line>
						<v-img
							aspect-ratio="2"
							contain
							height="50px"
							width="100px"
							src="../assets/JoJo's_Bizarre_Adventure_logo.png"
						>
						</v-img>
						<!-- カードが見たい時用
						<v-list-item-title>
							{{ item }}
						</v-list-item-title>
						-->
					</v-list-item>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
export default {
	name: 'Concentration-Game',
	data: function() {
		return {
			items: [],
			card: "",
			cards: [],
			cards_count: 2,
			getFlg: false
		};
	},
	mounted: function() {
		this.gameStart();
	},
	methods: {
		/*******************************************
		ゲーム開始
		*******************************************/
		gameStart: function() {
			// alert("貴様・・みているな！！ゲーム開始！")
			this.setData();
		},
		/*******************************************
		カード選択
		*******************************************/
		choiceCards: function(name) {
			// カードを配列に追加する
			this.cards.push(name);
			// カードのnameを取得(画面表示用)
			this.card = name;
			// 表示フラグを切り替え(画面表示用)
			this.getFlg = true;
			// 引ける残りカード枚数を-1
			this.cards_count--;
			// 引ける残りカード枚数が0の場合、ジャッジへ
			if (this.cards_count == 0) {
				// カード2枚分のnameが入った配列を渡す
				this.judgeCards(this.cards);
			}
		},
		/*******************************************
		カードのジャッジ
		*******************************************/
		judgeCards: function(cards) {
			// 一致の場合
			if (cards[0] == cards[1]) {
				alert("承太郎「やるじゃねぇか・・ジジイ」");
				// カードを削除する
				this.items.forEach((item, index) => {
					if(item === cards[0]) {
						this.items.splice(index, 1);
					}
				});
			// 不一致の場合
			} else {
				alert("DIO「バカめ！そのカードは" + this.card + "なんじゃあないのか？」");
			}
		this.setFlg();
		},
		/*******************************************
		カードの追加
		*******************************************/
		addCards: function() {
			// 2枚ずつカードを追加する
			for(let i = 0; i < 2; i++){
				this.items.push(
					"ポルナレフ",
					"ジョセフ",
					"JOJO",
					"キングクリムゾン",
					"スタープラチナ",
					// "スピードワゴン",
					// "DIO",
					// "空条承太郎"
				);
			}
		},
		/*******************************************
		カードのシャッフル
		*******************************************/
		shuffleCards: function(cards) {
			// 要素数分の乱数を作成
			const randomNumbers = [];
			for (let i = 0; i < cards.length; i++) {
				randomNumbers.push(Math.random());
			}
			const result = cards.sort((a, b) => {
				return randomNumbers[cards.indexOf(a)] - randomNumbers[cards.indexOf(b)]
			});
			this.items = result;
		},
		/*******************************************
		フラグの初期化
		*******************************************/
		setFlg: function() {
			this.cards = [];
			this.card = "";
			this.cards_count = 2;
			this.getFlg = false;
		},
		setData: function() {
			this.addCards();
			this.shuffleCards(this.items);
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
