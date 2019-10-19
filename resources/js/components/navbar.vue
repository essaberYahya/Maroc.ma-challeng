<template>
    <div>
    <header class="header" id="site-header">
        <div class="container">
                <div class="header-content-wrapper">
                    <div class="logo">
                        <div class="logo-text">
                            <div class="logo-title">Maroc.ma</div>
                        </div>
                    </div>

                    <nav id="primary-menu" class="primary-menu" style="float:right;">
                        <ul class="primary-menu-menu" style="overflow: hidden;">

                            <li class="" v-for="nav in navbar" v-bind:key="nav.object_id">
                                <a href="">{{ nav.label }}</a>
                            </li>
                        </ul>
                    </nav>

                </div>
        </div>
    </header>
    </div>
</template>
<script>
export default {
    mounted(){
        console.log('this run successfi');
    },
    data (){
        return {
            navbar : [],
            navbar : {
                Icon: '',
                color: '',
                id: '',
                label: '',
                object_id: ''
            },
            pagination : {}
        }

    },
    methods : {
        fetchNavbarData(){
            axios.get('http://femme.nextmedia.ma/api/menus/get_menu/?menu_id=7')
            .then((response) => {
                this.navbar = response.data.menu.output;
            })
        },
        makePagination(){

        }
    },
    created(){
        this.fetchNavbarData();
    }
}
</script>
