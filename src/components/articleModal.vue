<template>
    <div >
        <div class="modal-header">
            <h2 class="title">{{title}}</h2>
            <span class="close" @click="cancelArticleModal">&times;</span>
        </div>
         <form >
            <div class="modal-content-left" >
                <div class="form-group">
                    <label for="articleTitle" class="label">Title</label>
                    <input type="text" class="form-control" id="articleTitle" placeholder="Type title here..." v-model="modifiedArticle.articleTitle">
                </div>
                <div class="form-group">
                    <label for="articleText" class="label">Text</label>
                    <textarea class="form-control" id="articleText" rows="3" placeholder="Type title here..." v-model="modifiedArticle.articleText"></textarea>
                </div>
                <div class="form-group">
                    <label for="originalLink" class="label">Original Link</label>
                    <input type="text" class="form-control" id="originalLink" placeholder="Type link here..." v-model="modifiedArticle.originalLink">
                </div>
                <div class="form-group">
                    <label for="numberOfResponders" class="label">Number of Responders</label>
                    <span class="sliderNumber">{{modifiedArticle.numberOfResponders}}</span>
                    <input type="range" class="form-control-range" id="numberOfResponders" min="1" max="500" v-model="modifiedArticle.numberOfResponders">
                </div>
            </div>
            <div class="modal-content-right">
                 <div class="form-group">
                    <label for="location" class="label">Location</label>
                    <input type="text" class="form-control" id="location" placeholder="Type location here..." v-model="modifiedArticle.location">
                </div>
                <div class="form-group">
                    <label for="distance" class="label">Distance</label>
                    <span class="sliderNumber">{{modifiedArticle.distance}}</span>
                    <input type="range" class="form-control-range" id="distance" min="500" max="5000" step="50" v-model="modifiedArticle.distance">
                </div>
                <div class="form-group">
                    <label for="validityDate" class="label">Validity</label>
                    <input type="text" class="form-control" id="validityDate" placeholder="MM/DD/YYYY" v-model="modifiedArticle.validityDate">
                </div>
                 <div class="form-group">
                    <label for="age" class="label">Age</label>
                    <span class="sliderNumber">{{modifiedArticle.age}}</span>
                    <input type="range" class="form-control-range" id="age" min="18" max="110" v-model="modifiedArticle.age">
                </div>
                <div class="form-group">
                    <label for="gender" class="label">Gender</label>
                    <select class="form-control" id="gender" v-model="modifiedArticle.gender">
                        <option>Female</option>
                        <option>Male</option>
                        <option>Other</option>
                    </select>
                </div>
            </div>
        </form>
        <div class="modal-footer">
            <b-button @click="closeArticleModal"
                       class="btn"
                       variant="primary" >Save</b-button>
        </div>
    </div>
</template>

<script>
export default {
    name: "articleModal",
    props: ['title', 'article'],
    data(){
    return {
        modifiedArticle: {}
        };
    },
    methods: {
        closeArticleModal(){            
            this.$emit('closeArticleModal', this.modifiedArticle);
        },
        cancelArticleModal(){
            this.$emit('cancelArticleModal');
        }
    },
    created(){        
        this.modifiedArticle = this.article;           
    }
}
</script>

<style scoped>
    .title{
        float: left;
    }
    .header{
        margin: 10px;
    }

    .close {
        color: #aaa;
        float: right;
        font-size: 28px;
        font-weight: bold;
    }

    .close:hover,
    .close:focus {
        color: black;
        text-decoration: none;
        cursor: pointer;
    }
   
   .modal-header {
        padding: 2px 16px;
        color: black;
        border: none;
    }

    .modal-body {
        padding: 2px 16px;
        background-color: #fefefe;        
    }

    .modal-footer {
        position: relative;
        width: 100%;
        border: none;       
    }

    .modal-content-left{
        float: left;
        height: auto;
        width: 48%;
        margin-right: 30px;
    }

     .modal-content-right{
        float: right;
        height: auto;
        width: 48%;
    }

    .label{
        float: left;
    }

    .sliderNumber{
        margin-left: 10px;
        font-weight: bold;
        float: left;

    }
    

</style>