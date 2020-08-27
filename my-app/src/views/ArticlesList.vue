<template>
  <b-container>
    <div class="row my-5">
      <h1>On en parle !</h1>
    </div>

    <Searchbar />

    <b-row cols="1" cols-lg="2" cols-md="1" cols-sm="1">
      <Article
        v-for="article in articlesList"
        :article="article"
        :key="article.id"
        :articlesList="articlesList"
      />
    </b-row>
  </b-container>
</template>


<script>
import Article from "@/components/ArticlePresentation.vue";
import Searchbar from "@/components/Searchbar.vue";
import firebase from "firebase";

export default {
  components: {
    Article,

    Searchbar,
  },
  data() {
    return {
      articlesList: [],
      search: "",
      articleTags: [],
      selectedTag: "",
      itemOrderBy: "id",
    };
  },
  created() {
    this.articlesList = this.display();
    console.log("le pb est ici!");
    console.log("1: " + this.articlesList.length);
    this.displayPropTags(this.articleTags);
  },
  mounted: function () {
    //this.articlesList = this.$store.getters.articles;
  },
  computed: {
    /*sortArrays(arrays) {
      return _.orderBy(arrays, this.itemOrderBy, "asc");
    },*/
  },
  methods: {
    displayPropTags(list) {
      let ref = firebase.database().ref("tags");
      ref.once("value", function (snapshot) {
        snapshot.forEach(function (childSnapshot) {
          var childKey = childSnapshot.key;
          console.log(childKey);
          list.push(childKey);
        });
      });
      console.log(list.length);
    },
    searchArticleByText() {
      console.log(this.search);
      console.log(this.selectedTag);
    },
    display() {
      var list = [];
      let ref = firebase.database().ref("articles");
      ref.once("value", function (snapshot) {
        snapshot.forEach(function (childSnapshot) {
          var childKey = childSnapshot.key;
          var childData = childSnapshot.val();
          const article = {
            id: childKey,
            title: childData.title,
            abstract: childData.abstract,
            releaseDate: childData.releaseDate,
            picture: childData.picture,
          };
          console.log(article);
          list.push(article);
        });
      });
      console.log(list.length);
      return list;
    },
  },
};
</script>