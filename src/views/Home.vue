<template>
  <div class="home" >
      <div class="add-btn-div">
        <b-button class="add-btn"                  
                  @click="showArticleModal(null)">                  
                  Add Article
        </b-button>
      </div>
      <table class="table table-sm table-bordered" >
        <thead class="thead thead-dark">
          <tr scope="row">
            <th scope="col">Title</th>
            <th scope="col">Text</th>
            <th scope="col">Published</th>
            <th scope="col">Edit/Delete</th>
          </tr>
        </thead>
        <tbody v-for="article in articles" :key=article.id
               class=" table-striped"> 
          <tr scope="row">
            <td >{{article.articleTitle}}</td>
            <td class="colBody">{{article.articleText}}</td>
            <td >{{article.published}}</td>
            <td >
              <span class="editdelete">
                <img class="imgSize" 
                     src="../assets/editX2.png"
                     @click="showArticleModal(article)">
              </span>
              <span  class="editdelete">
                <img class="imgSize" 
                     src="../assets/deleteX2.png"
                     @click="deleteArticle(article.id)">
              </span>
            </td>
          </tr>
        </tbody>
      </table>
      <div class="articleModal" v-if="articleModalVisible">
        <ArticleModal v-bind:title="articleModalTitle" 
                      v-bind:article="selectedArticle"
                      v-on:closeArticleModal="closeArticleModal"
                      v-on:cancelArticleModal="hideArticleModal"
                      class="articleModal-content"/>
      </div>
  </div>
</template>

<script>
import ArticleModal from '../components/articleModal';
import Moment from 'moment';

export default {
  name: "Home",
  components: {
    ArticleModal
  },
  data(){
    return {
      articles: [],
      articleModalVisible: false,
      articleModalTitle: '',
      selectedArticle: {}
    };
  },
  methods: {
    async fetchArticles() {
      const res = await fetch('articles.json');
      const val = await res.json();
      val[0].published = Moment().toLocaleString();
      val[1].published = Moment().toLocaleString();
      this.articles = val;
    },
    showArticleModal(article){
      if(article !== null){
        this.articleModalTitle = 'Edit Article';
        this.selectedArticle = article;
      }
      else{
        this.articleModalTitle = 'Add Article';
        this.selectedArticle = {
                id: 0,
                articleTitle: "",
                articleText: "",
                originalLink: "",
                numberOfResponders: "",
                location: "",
                distance: "",
                validityDate: "",
                age: 0,
                gender: null,
                published: null
        };
      }
      this.articleModalVisible = true;
    },
    hideArticleModal(){
      this.articleModalVisible = false;
    },
    closeArticleModal(article){
      if(article.id === 0){
        article.id = this.articles.length + 1;
        article.published = Moment().toLocaleString();
        this.articles.push(article);
      }
      this.hideArticleModal();
    },
    deleteArticle(id){
      this.articles = this.articles.filter(a => a.id !== id);
    }
  },
  created(){
    this.fetchArticles();
  }
};
</script>

<style scoped>
  .add-btn-div{
    width: 100%;
  }

  .add-btn{
    float: right;
    margin: 10px;
  }

  .colBody{
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    max-width: 500px;
  }

.articleModal { 
  position: fixed; 
  z-index: 1; 
  left: 0;
  top: 0;
  width: 100%; 
  height: 100%; 
  overflow: unset; 
  background-color: rgb(0,0,0,0.6);
}

.editdelete{
  margin: 6px;
}
.imgSize{
  height: 70%;
  width: auto;
}
  .articleModal-content {
    background-color: #fefefe;
    margin: 15% auto; 
    padding: 20px;
    border: 1px solid #888;
    border-radius: 10px;
    width: 80%; 
    height: auto;
    overflow: auto;
    animation-name: animatetop;
    animation-duration: 1s
  }

    @keyframes animatetop {
      from {opacity: 0}
      to {opacity: 1}
    }
</style>
