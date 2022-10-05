<template>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
        <div class="container-fluid">
            <div class="row">
                <div class="col-lg-12 mt-5" v-if="products.length > 0">
                    <carousel class="product-slider" :autoplay="true" :dots="false" :margin="15" :nav="false">

                        <div class="product-item" v-for="itemProduct in products" v-bind:key="itemProduct.id">
                            <div class="pi-pic">
                                <!-- <img v-bind:src="'img/products/'+itemProduct.name+'.jpg'" alt=""> -->
                                <img v-bind:src="'http://127.0.0.1:8001/storage/'+itemProduct.photo" alt="">
                                <router-link v-bind:to="'/product/'+itemProduct.products_id">
                                    <ul>
                                        <li class="w-icon acti ve">
                                            <!-- <a href="#"><i class="icon_bag_alt"></i></a> -->
                                        </li>
                                        <li class="quick-view"><a>+ Quick View</a></li>
                                    </ul>
                                </router-link>
                            </div>
                            <div class="pi-text">
                                <div class="catagory-name">{{itemProduct.type}}</div>
                                <a href="#">
                                    <h5>{{itemProduct.name}}</h5>
                                </a>
                                <div class="product-price">
                                    ${{itemProduct.price}}
                                </div>
                            </div>
                        </div>

                    </carousel>
                </div>
                <div class="col-lg-12 mt-5" v-else>
                    <p>Product Belum Tersedia</p>
                </div>
            </div>
        </div>
    </section>
    <!-- Women Banner Section End -->
</template>

<script>
import carousel from 'vue-owl-carousel';
import axios from 'axios';

export default {
    name: "HomeProd",
    components: {
        carousel,
    },
    data() {
        return {
            products: []
        };
    },
    mounted() {
        axios
            .get("http://127.0.0.1:8001/api/products")
            .then(res => (this.products = res.data.data.data))
            .catch(err => console.log(err));
    }
}
</script>