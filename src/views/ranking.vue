<template>
  <!-- 楽天レシピカテゴリ別ランキングAPI利用 -->
  <div class="about">
    <HelloWorld msg="カテゴリ別のランキングを見る" />
    <p>カテゴリ別のランキングを４位まで見ることが出来ます。</p>
    <form class="form_style">
      <label class="ranking_category">カテゴリ</label>
      <!-- optionで選択されたオブジェクトを受け取る -->
      <select name="large" id="large" v-model="getranking_category">
        <!-- valueで選択されたオブジェクトを渡す -->
        <option
          v-for="category in look_rankingData"
          v-bind:key="category.categoryId"
          v-bind:value="category"
        >
          <!-- カテゴリー名表示 -->
          {{ category.categoryName }}
        </option>
      </select>
      <button
        v-on:click.prevent="sampleRecipe_look()"
        v-on:click.once="click_show = !click_show"
        class="look_btn"
      >
        ランキング上位を見る
      </button>
    </form>
    <transition-group tag="div">
      <!-- 取得したランキング結果をtable表示 -->
      <div
        v-for="look in looks"
        v-bind:key="look.recipeId"
        class="ranking-content"
      >
        <img class="ranking_food-img" v-bind:src="look.foodImageUrl" />
        <table border="1">
          <thead>
            <tr>
              <th colspan="3" class="tb_recipe-title">
                《 第{{ look.rank }}位 》
                {{ look.recipeTitle }}
              </th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>
                <p>《材料費》</p>
                {{ look.recipeCost }}
              </td>
              <td>
                <p>《目安時間》</p>
                {{ look.recipeIndication }}
              </td>
              <td>
                <p>《材料》</p>
                <span
                  v-for="material in look.recipeMaterial"
                  v-bind:key="material.index"
                >
                  ・{{ material }}
                </span>
              </td>
            </tr>
            <tr>
              <td colspan="3" class="tb_recipe-description">
                {{ look.recipeDescription }}
              </td>
            </tr>
            <tr>
              <td colspan="3" class="tb_recipe-link">
                <a v-bind:href="look.recipeUrl" target="_blank">{{
                  look.recipeUrl
                }}</a>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </transition-group>
    <div v-show="click_show">
      <p>４位以降のレシピも見ることが出来ます。</p>
      <button class="more_look">
        <a
          v-bind:href="getranking_category.categoryUrl"
          target="_blank"
          rel="noopener noreferrer"
          >もっとレシピを見る</a
        >
      </button>
    </div>
  </div>
</template>

<script>
import HelloWorld from "@/components/HelloWorld.vue";
import axios from "axios";

export default {
  name: "ranking",
  components: {
    HelloWorld,
  },
  data: function () {
    return {
      looks: [],
      look_rankingData: [],
      getranking_category: {},
      click_show: false,
      more_rankingRecipe: "",
    };
  },
  // 要素にmountフックしたときに、楽天レシピAPIからカテゴリ一毎のデータを取得
  mounted() {
    axios
      .get(
        "https://app.rakuten.co.jp/services/api/Recipe/CategoryList/20170426?applicationId=1083372515077401243&categoryType=large"
      )
      // データ取得が成功したらlook_rankingDataに代入
      .then((response) => {
        this.look_rankingData = response.data.result.large;
      })
      // エラーならエラー表示
      .catch((err) => console.log(err));
  },
  methods: {
    sampleRecipe_look() {
      axios
        .get(
          "https://app.rakuten.co.jp/services/api/Recipe/CategoryRanking/20170426?applicationId=1083372515077401243&categoryId=" +
            // formにてvalueが動的に変更される
            // 選択されているオブジェクトのcategoryIdをキーとして使う
            this.getranking_category["categoryId"]
        )
        .then((Target) => {
          // カテゴリー毎のランキング上位４位までを取得
          this.looks = Target.data.result;
        })
        // エラー処理
        .catch((err) => console.log(err));

      // this.more_rankingRecipe = this.
    },
  },
};
</script>

<style scoped>
.ranking_food-img {
  width: 100%;
  height: 500px;
  display: block;
  margin: 20px auto;
  object-fit: contain;
  /* vueのassetsフォルダ内のimgを参照する場合
  、~@/assetsから始めないと表示されない */
  background-image: url("~@/assets/bg-recipe.png");
  background-size: 100%;
}
.ranking-content {
  margin: 70px auto;
  width: 70%;
}
table {
  width: 100%;
  background-color: rgb(255, 247, 206);
  table-layout: fixed;
}
td {
  min-width: 150px;
  padding: 10px;
}
.tb_recipe-title,
.tb_recipe-description,
.tb_recipe-link {
  padding: 20px 10px;
}

.form_style {
  padding: 20px 5px 30px;
}
.more_look {
  width: 230px;
  height: 50px;
  color: #000;
  font-weight: bold;
  background-color: #fff;
  border: 2px solid #ff6666;
  border-radius: 5px;
  padding: 5px 15px;
  margin-top: 15px;
  transition-duration: 1s;
}
.more_look:hover {
  transform: scale(1.1);
  background: #ff6666;
  font-weight: bold;
  color: #fff;
}
.more_look > a {
  display: block;
  color: #000;
  text-decoration: none;
}
.more_look:hover,
.more_look > a:hover {
  color: #fff;
}
.look_btn {
  width: 30%;
}
.v-enter,
.v-leave-to {
  opacity: 0;
}
.v-enter-active,
.v-leave-active {
  transition: opacity 1s;
}
@media screen and (max-width: 1200px) {
  .look_btn {
    width: 52%;
  }
}
@media screen and (max-width: 900px) {
  .ranking-content {
    margin: 50px auto;
  }
}
@media screen and (max-width: 680px) {
  .ranking-content {
    width: 80%;
  }
  .look_btn {
    width: 60%;
    height: 70px;
  }
}
@media screen and (max-width: 480px) {
  td {
    padding: 0;
  }
}
</style>
