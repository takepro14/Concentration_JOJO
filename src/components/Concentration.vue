<template>
	<!--
		全体を囲むコンテナ, 背景
	-->
	<v-container
		class="bg"
	>
		<!--
			タイトル
		-->
		<v-row>
			<v-col>
				<h1>
					ジョジョの奇妙な神経衰弱
				</h1>
			</v-col>
		</v-row>
		<!--
			ゲームリセットボタン, カード選択枚数
		-->
		<v-row>
			<v-col>
				<v-btn
					elevation="2"
					@click="gameStart"
					x-large
				>
					ゲームをリセットォォ！
				</v-btn>
			</v-col>
			<v-col>
				<v-card-title>
					カードを選んでください。残り {{ cardsCount }} 枚
				</v-card-title>
			</v-col>
		</v-row>

		<!--
			カード一覧
		-->
		<v-row
			justify="center"
			align-content="center"
		>
			<!--
				ダイアログブロック
			-->
			<v-dialog
				v-model="dialog"
				width="500"
			>
				<!--
					カード(裏面)
				-->
				<template v-slot:activator="{ on, attrs }">
					<v-col
						cols="6" sm="4" md="3" lg="2"
						v-for="(card, index) in cardsAll"
						:key="index"
					>
					{{card.img}}
						<v-card
							class="d-inline-flex pa-2"
							elevation="2"
							color="deep-purple lighten-3"
							outlined
							shaped
							height="100"
							max-width="200"
							v-on="on"
							v-bind="attrs"
							@click="getCard(card)"
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
							</v-list-item>
						</v-card>
					</v-col>
				</template>

				<!--
					カード(表面)
				-->
				<v-card>
					<v-card-title
						class="text-h5 grey lighten-2"
					>
						{{ card.name }}
					</v-card-title>

					<v-card-text>
						{{ card.msg }}
					</v-card-text>

					<v-list-item three-line>
						<v-img
							aspect-ratio="2"
							contain
							:src="card.src"
						>
						</v-img>
					</v-list-item>

					<v-divider></v-divider>

					<v-card-actions>
						<v-spacer></v-spacer>
						<v-btn
							color="primary"
							text
							@click="dialog = false"
						>
							閉じる
						</v-btn>
					</v-card-actions>
				</v-card>
			</v-dialog>
		</v-row>
	</v-container>
</template>

<script>
export default {
	name: 'Concentration-Game',
	data() {
		return {
			// 引いたカードのオブジェクト
			card: "",
			// 引いたカード(2枚)のオブジェクト
			cards: [],
			// 全カードのコレクション
			cardsAll: [],
			// カードを引ける残数
			cardsCount: 2,
			// getFlg: false,
			// モーダルの表示切り替え
			dialog: false,
		};
	},
	mounted() {
		this.gameStart();
	},
	methods: {
		/*******************************************
		ゲーム開始
		*******************************************/
		gameStart() {
			this.setFlg();
			this.setData();
		},
		/*******************************************
		カード選択
		*******************************************/
		// item: 引いたカード1枚 {...}
		getCard(item) {
			// 引いたカード(obj)を表示用の変数に代入する
			this.card = item;
			// 引いたカード(obj)を配列に追加する
			this.cards.push(item);
			// 引ける残りカード枚数を-1
			this.cardsCount--;
			// 引ける残りカード枚数が0の場合、ジャッジへ
			if (this.cardsCount == 0) {
				// カード2枚分のnameが入った配列を渡す
				this.judgeCards(this.cards);
			}
		},
		/*******************************************
		カードのジャッジ
		*******************************************/
		// items: 引いたカードリスト [{...}, {...}]
		judgeCards(items) {
			// 一致の場合
			if (items[0].name == items[1].name) {
				alert("承太郎「やるじゃねぇか・・ジジイ」");
				// カードを削除する: 全カードのnameを今カードのnameを順番に照合
				this.cardsAll.forEach((item, index) => {
					if(item.name === items[0].name) {
						this.cardsAll.splice(index, 2);
					}
				});
			// 不一致の場合
			} else {
				alert("DIO「バカめ！そのカードは" + this.card.name + "なんじゃあないのか？」");
			}
		// フラグの初期化
		this.setFlg();
		},
		/*******************************************
		カードの追加
		*******************************************/
		addCards() {
			// 2枚ずつカードを追加する
			for(let i = 0; i < 2; i++){
				this.cardsAll.push(
					{
						name: "ポルナレフ",
						msg: "あ・・・ありのまま今起こった事を話すぜ！",
						src: require("../assets/pornalev.jpg")
					},
					{
						name: "承太郎",
						msg: "あまりなめた態度とるんじゃあねーぜ。おれはやると言ったらやる男だぜ・・！",
						src: require("../assets/jotaro.jpg")
					},
					{
						name: "DIO",
						msg: "URYYYYYYYYYYYYYYY!!!!",
						src: require("../assets/dio.jpg")
					},
					{
						name: "ディアボロ",
						msg: "この『キング・クリムゾン』の前では何者だろうとその「動き」は無意味となる！！",
						src: require("../assets/king-crimson.jpg")
					},
				);
			}
		},
		/*******************************************
		カードのシャッフル
		*******************************************/
		shuffleCards(items) {
			// 要素数分の乱数を作成
			const randomNumbers = [];
			for (let i = 0; i < items.length; i++) {
				randomNumbers.push(Math.random());
			}
			const result = items.sort((a, b) => {
				return randomNumbers[items.indexOf(a)] - randomNumbers[items.indexOf(b)]
			});
			this.items = result;
		},
		/*******************************************
		フラグの初期化
		*******************************************/
		setFlg() {
			this.card = "";
			this.cards = [];
			this.cardsCount = 2;
			this.dialog = false;
		},
		setData() {
			this.cardsAll = [];
			this.addCards();
			this.shuffleCards(this.cardsAll);
		}
	}

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bg {
	background-image: url("~@/assets/morioh-cho.jpg");
	background-size: cover;
	height: 1000px;
}
/* 背景画像設定のメモ */
/* https://qiita.com/HaruPON/items/60cac14348dc70a050c7 */

.flex-container {
	display: flex;
	justify-content: center;
}

/* 0.5秒かけて表示する */
.transit-enter-active {
	transition: opacity 0.5s;
}
/* opacity:0(透明)から */
.transit-enter {
	opacity: 0;
}
/* opacity:1(透明なし)にする */
.transit-enter-to {
	opacity: 1.0;
}

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
