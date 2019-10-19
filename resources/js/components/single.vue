<template>
    <div>
        <div class="stunning-header stunning-header-bg-lightviolet">
            <div class="stunning-header-content">
                <h1 class="stunning-header-title">{{ this.single.title }}</h1>
            </div>
        </div>
        <div class="loading text-center mt-3" v-if="!this.loaded">
            <div class="spinner text-center">
                <div class="double-bounce1"></div>
                <div class="double-bounce2"></div>
            </div>
        </div>
        <div class="container" v-if="this.loaded">
        <div class="row medium-padding120">
        <main class="main">
            <div class="col-lg-10 col-lg-offset-1">
                <article class="hentry post post-standard-details">

                    <div class="post-thumb">
                        <img v-bind:src="this.single.thumbnail_images.large.url" alt="" srcset="">
                    </div>

                    <div class="post__content">


                        <div class="post-additional-info">



                            <span class="post__date">

                                <i class="seoicon-clock"></i>

                                <time class="published">
                                    {{ single.date }}
                                </time>

                            </span>

                            <span class="category">
                                <i class="seoicon-tags"></i>
                                <a href="#">Business,</a>
                                <a href="#">Seo</a>
                            </span>

                        </div>

                        <div class="post__content-info text-right" >


                            <div class="testimonial-item quote-left">

                                <h5 class="h5 testimonial-text" v-html="single.title">
                                    {{ single.title }}
                                </h5>

                                <div class="author-info-wrap table">
                                    <div class="author-info table-cell">
                                        <h6 class="author-name c-primary">Angelina Johnson</h6>
                                        <div class="author-company">Envato Market</div>
                                    </div>
                                </div>

                                <div class="quote">
                                    <i class="seoicon-quotes"></i>
                                </div>

                            </div>

                            <p class="post__text" v-html="single.content">
                                {{ single.content }}
                            </p>

                            <h4 class="mb30">مقتطفات</h4>


                            <ul class="list list--secondary">


                                <li>
                                    <i class="seoicon-check"></i>
                                    <a href="#" v-html="single.excerpt">
                                        {{ single.excerpt }}
                                    </a>
                                </li>

                            </ul>


                        </div>
                    </div>

                    <div class="socials">Share:
                        <a href="#" class="social__item">
                            <i class="seoicon-social-facebook"></i>
                        </a>
                        <a href="#" class="social__item">
                            <i class="seoicon-social-twitter"></i>
                        </a>
                        <a href="#" class="social__item">
                            <i class="seoicon-social-linkedin"></i>
                        </a>
                        <a href="#" class="social__item">
                            <i class="seoicon-social-google-plus"></i>
                        </a>
                        <a href="#" class="social__item">
                            <i class="seoicon-social-pinterest"></i>
                        </a>
                    </div>

                </article>



            </div>


            <!-- End Sidebar-->

        </main>
    </div>
</div>
    </div>
</template>
<script>
export default {
    props : ['id'],
    mounted(){

    },
    data () {
      return {
          single : [],
          loaded : false
      }
    },
    methods : {
        fetchSinglePost(){
            axios.get('http://femme.nextmedia.ma/api/get_post/?id='+this.id)
            .then((response) => {

                this.single = response.data.post
            }).then((response) => {
                this.loaded = true;
            })
        }
    },
    created(){
        this.fetchSinglePost();
    }
}
</script>
