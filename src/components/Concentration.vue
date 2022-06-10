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
		カード選択時ダイアログ
		-->
		<v-row>
			<v-col>
				<ul>
					<transition name="transit">
						<v-alert
							v-show="getFlg"
							border="bottom"
							color="pink darken-1"
							dark
						>
							<li>承太郎「おいジジイ、そりゃあ {{ card }} のカードだぞ」</li>
						</v-alert>
					</transition>
				</ul>
			</v-col>
		</v-row>
		<!--
		リセットボタン, カード選択枚数
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
					カードを選んでください。残り {{ cards_count }} 枚
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
			<v-dialog
				v-model="dialog"
				width="500"
				>
				<!--
				カード(裏面) ... アクティベータースロット
				-->
				<template v-slot:activator="{ on, attrs }">
					<v-col
						cols="6" sm="4" md="3" lg="2"
						v-for="(value, key, index) in items"
						:key="index"
					>
					{{ key }} is {{ value.name }}
						<v-card
							class="d-inline-flex pa-2"
							elevation="2"
							color="deep-purple lighten-3"
							outlined
							shaped
							height=100
							max-width="200"
							v-on="on"
							v-bind="attrs"
						>
						<!-- @click="choiceCards(item) "-->
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
				カード(表面) ... ダイアログコンテンツ
				-->
				<v-card>
					<v-card-title
						class="text-h5 grey lighten-2"
					>
						DIO
					</v-card-title>

					<v-card-text>
						貧弱貧弱ゥ！！
					</v-card-text>

					<v-list-item three-line>
						<v-img
							aspect-ratio="2"
							contain
							src="../assets/dio.jpg"
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
	data: function() {
		return {
			items: [],
			card: "",
			cards: [],
			cards_count: 2,
			getFlg: false,
			dialog: false
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
			this.setFlg();
			this.setData();
		},
		/*******************************************
		カード選択
		*******************************************/
		choiceCards: function(name) {
			// モーダルを閉じる
			// this.dialog = false
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
						this.items.splice(index, 2);
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
					{name: "ポルナレフ", msg: "ポルナレフ〜"},
					{name: "ジョジョ", msg: "ジジィ。。"},
					{name: "DIO", msg: "貧弱貧弱"},
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
