<template>
    <div>
        <div class="">
            <nav aria-label="Page navigation example">
                <ul class="pagination">
                    <li class="page-item"><a class="page-link" href="#" @click="makePaginationDown()">Previous</a></li>
                    <li class="page-item disabled"><a class="page-link" href="#">{{ this.paginate +'/'+  this.all.pages }}</a></li>

                    <li class="page-item"><a class="page-link" href="#" @click="makePaginationUp()">Next</a></li>
                </ul>
            </nav>
        </div>
        <br><br><br><br>
        <div class="loading text-center" v-if="!this.loaded">
            <div class="spinner text-center">
                <div class="double-bounce1"></div>
                <div class="double-bounce2"></div>
            </div>
        </div>
        <div class="posts" v-if="this.loaded">
            <article class="hentry post post-standard has-post-thumbnail sticky" v-for="post in posts" v-bind:key='post.id'>

                    <div class="post-thumb">
                            <img v-bind:src="post.thumbnail_images.large.url" alt="seo">
                            <div class="overlay"></div>
                            <a bind-href="post.thumbnail_images.large.url" class="link-image js-zoom-image">
                                <i class="seoicon-zoom"></i>
                            </a>
                            <a href="#" class="link-post">
                                <i class="seoicon-link-bold"></i>
                            </a>
                    </div>

                    <div class="post__content">

                            <div class="post__content-info text-right">

                                    <h2 class="post__title entry-title ">
                                        <a :href="'/single/'+post.id">{{ post.title }}</a>
                                    </h2>

                                    <div class="post-additional-info">

                                        <span class="post__date">

                                            <i class="seoicon-clock"></i>

                                            <time class="published" datetime="2016-04-17 12:00:00">
                                                {{ post.date }}
                                            </time>

                                        </span>



                                    </div>
                            </div>

                    </div>
            </article>
        </div>
    </div>
</template>
<script>
export default {
    mounted(){

    },
    data(){
        return{
            posts : [],
            all : [],
            post : {
                title : '',
                content : '',
                url : '',
                id : ''
            },
            loaded : false,
            paginate : 1
        }
    },
    created(){
        this.fetchAllArticles();

    },
    methods : {
        fetchAllArticles(page){

            let vm = this
            page = page || this.paginate;
            axios.get(' http://femme.nextmedia.ma/api/get_recent_posts/?page='+page,{ mode: "no-cors" })
            .then((response) => {
                this.posts = response.data.posts;
                this.all = response.data;
            }).then((response) => {
                this.loaded = true;
            })
        },
        makePaginationUp(){
            this.loaded=false;
            var pa = ++this.paginate;
            this.fetchAllArticles(pa);
             this.loaded=true;
        },
        makePaginationDown(){
            this.loaded=false;
            var pa = --this.paginate;
            this.fetchAllArticles(pa);
             this.loaded=true;
        }
    }
}
</script>
