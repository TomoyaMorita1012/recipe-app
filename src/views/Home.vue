<template>
  <div class="home">
    <HelloWorld msg="カテゴリ・材料から探す" />
    <p>ここからレシピを検索出来ます。</p>
    <form
      v-bind:action="recipe_url"
      class="form_style"
      target="_blank"
      rel="noopener noreferrer"
    >
      <label>カテゴリ別</label>
      <select name="large" id="large" v-model="recipe_url">
        <option
          v-for="recipe in large_data"
          v-bind:key="recipe.categoryId"
          v-bind:value="recipe.categoryUrl"
        >
          {{ recipe.categoryName }}
        </option>
      </select>
      <button type="submit" class="look_btn">
        <span>レシピを見る</span>
      </button>
    </form>
    <form
      v-bind:action="recipe_url"
      class="form_style"
      target="_blank"
      rel="noopener noreferrer"
    >
      <label>材料別(大まか)</label>
      <select name="medium" id="medium" v-model="recipe_url">
        <option
          v-for="recipe in medium_data"
          v-bind:key="recipe.categoryId"
          v-bind:value="recipe.categoryUrl"
        >
          {{ recipe.categoryName }}
        </option>
      </select>
      <button type="submit" class="look_btn"><span>レシピを見る</span></button>
    </form>
    <form
      v-bind:action="recipe_url"
      class="form_style"
      target="_blank"
      rel="noopener noreferrer"
    >
      <label>材料別(詳細)</label>
      <select name="small" id="small" v-model="recipe_url">
        <option
          v-for="recipe in small_data"
          v-bind:key="recipe.categoryId"
          v-bind:value="recipe.categoryUrl"
        >
          {{ recipe.categoryName }}
        </option>
      </select>
      <button type="submit" class="look_btn"><span>レシピを見る</span></button>
    </form>
    <p class="add_direction">
      楽天会員の方はリンク先でログインすることをオススメします。<br />ログインすることでレシピをお気に入りに登録することが出来ます。
    </p>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    HelloWorld,
  },
  data: function () {
    return {
      recipes: [],
      large_data: [],
      medium_data: [],
      small_data: [],
      recipe_url: "",
    };
  },
  mounted() {
    axios
      .get(
        "https://app.rakuten.co.jp/services/api/Recipe/CategoryList/20170426?applicationId=1083372515077401243"
      )
      .then((response) => {
        this.recipes = response.data.result;
        this.large_data = this.recipes.large;
        this.medium_data = this.recipes.medium;
        this.small_data = this.recipes.small;
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style scoped>
button {
  margin: 10px;
}

.add_direction {
  width: 50%;
  padding: 10px;
  margin: 20px auto 30px;
  background-color: rgb(253, 248, 224);
  border: 3px solid #fcc277c2;
}

@media screen and (max-width: 680px) {
  .add_direction {
    width: 60%;
  }
}
</style>
