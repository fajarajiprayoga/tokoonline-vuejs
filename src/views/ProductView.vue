<template>
    <div class="productview">
        <HeaderVue />
        <!-- Breadcrumb Section Begin -->
        <div class="breacrumb-section">
            <div class="container">
                <div class="row">
                    <div class="col-lg-12">
                        <div class="breadcrumb-text product-more text-left">
                            <router-link to="/">
                                <i class="fa fa-home"></i> Home
                            </router-link>
                            <span>Detail</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- Breadcrumb Section Begin -->

        <!-- Product Shop Section Begin -->
        <section class="product-shop spad page-details">
            <div class="container">
                <div class="row">
                    <div class="col-lg-12">
                        <div class="row">
                            <div class="col-lg-6">
                                <div class="product-pic-zoom">
                                    <!-- <img class="product-big-img" :src="gambar_default" alt="" /> -->
                                    <img v-bind:src="'http://127.0.0.1:8001/storage/'+productDetails.photo"
                                        alt="http://127.0.0.1:8001/storage/assets/product/JRFqqbwOzKIbYVFiI9TV1HPnkpXNg8Fjcd5qhpuD.jpg">
                                </div>
                                <div class="product-thumbs">
                                    <carousel class="product-thumbs-track ps-slider" :items="3" :nav="false"
                                        :margin="8">
                                        <div class="pt" @click="(changeImage(thumbs[0]))"
                                            :class="thumbs[0] == gambar_default ? 'active' : 'nonactive'">
                                            <!-- <img src="img/products/women-1.jpg" alt="" /> -->
                                            <img v-bind:src="'http://127.0.0.1:8001/storage/'+productDetails.photo">
                                        </div>

                                        <div class="pt" @click="(changeImage(thumbs[1]))"
                                            :class="thumbs[1] == gambar_default ? 'active' : 'nonactive'">
                                            <!-- <img src="img/products/women-2.jpg" alt="" /> -->
                                            <img v-bind:src="'http://127.0.0.1:8001/storage/'+productDetails.photo">
                                        </div>

                                        <div class="pt" @click="(changeImage(thumbs[2]))"
                                            :class="thumbs[2] == gambar_default ? 'active' : 'nonactive'">
                                            <!-- <img src="img/products/women-3.jpg" alt="" /> -->
                                            <img v-bind:src="'http://127.0.0.1:8001/storage/'+productDetails.photo">
                                        </div>

                                        <div class="pt" @click="(changeImage(thumbs[3]))"
                                            :class="thumbs[3] == gambar_default ? 'active' : 'nonactive'">
                                            <!-- <img src="img/products/women-4.jpg" alt="" /> -->
                                            <img v-bind:src="'http://127.0.0.1:8001/storage/'+productDetails.photo">
                                        </div>
                                    </carousel>
                                </div>
                            </div>
                            <div class="col-lg-6 text-left">
                                <div class="product-details">
                                    <div class="pd-title">
                                        <span>{{productDetails.type}}</span>
                                        <h3>{{productDetails.name}}</h3>
                                    </div>
                                    <div class="pd-desc">
                                        <p>
                                            Lorem ipsum dolor sit amet consectetur adipisicing elit. Corporis, error
                                            officia.
                                            Rem aperiam laborum voluptatum vel, pariatur modi hic provident eum iure
                                            natus quos
                                            non a sequi, id accusantium! Autem.
                                        </p>
                                        <p>
                                            Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quam possimus
                                            quisquam
                                            animi, commodi, nihil voluptate nostrum neque architecto illo officiis
                                            doloremque et
                                            corrupti cupiditate voluptatibus error illum. Commodi expedita animi nulla
                                            aspernatur.
                                            Id asperiores blanditiis, omnis repudiandae iste inventore cum, quam sint
                                            molestiae
                                            accusamus voluptates ex tempora illum sit perspiciatis. Nostrum dolor
                                            tenetur amet,
                                            illo natus magni veniam quia sit nihil dolores.
                                            Commodi ratione distinctio harum voluptatum velit facilis voluptas animi non
                                            laudantium, id dolorem atque perferendis enim ducimus? A exercitationem
                                            recusandae
                                            aliquam quod. Itaque inventore obcaecati, unde quam
                                            impedit praesentium veritatis quis beatae ea atque perferendis voluptates
                                            velit
                                            architecto?
                                        </p>
                                        <h4>${{productDetails.price}}</h4>
                                    </div>
                                    <div class="quantity">
                                        <router-link to="/cart">
                                            <a @click="saveKeranjang(productDetails.products_id, productDetails.name, productDetails.price, productDetails.photo)"
                                                href="#" class="primary-btn pd-cart">Add To Cart</a>
                                        </router-link>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <!-- Product Shop Section End -->
        <RelatedProduct />
        <FooterVue />
    </div>
</template>

<script>
import HeaderVue from '@/components/HeaderVue.vue';
import FooterVue from '@/components/FooterVue.vue';
import carousel from 'vue-owl-carousel';
import RelatedProduct from '@/components/RelatedProduct.vue';
import axios from 'axios';


export default {
    name: 'ProductView',
    components: {
        HeaderVue,
        FooterVue,
        carousel,
        RelatedProduct
    },
    data() {
        return {
            gambar_default: "",
            thumbs: [
                "img/products/women-1.jpg",
                "img/products/women-2.jpg",
                "img/products/women-3.jpg",
                "img/products/women-4.jpg"
            ],
            productDetails: [],
            keranjangUser: []
        }
    },
    methods: {
        changeImage(urlImage) {
            this.gambar_default = urlImage;
        },
        setDataPicture(data) {
            this.productDetails = data;
            this.gambar_default = 'img/products/' + data.name + '.jpg'
        },
        saveKeranjang(idProduct, nameProduct, priceProduct, photoProduct) {

            var productStored = {
                "id": idProduct,
                "name": nameProduct,
                "price": priceProduct,
                "photo": 'http://127.0.0.1:8001/storage/' + photoProduct
            }

            this.keranjangUser.push(productStored);
            const parsed = JSON.stringify(this.keranjangUser);
            localStorage.setItem('keranjangUser', parsed);
        }
    },
    mounted() {
        if (localStorage.getItem('keranjangUser')) {
            try {
                this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
            } catch (e) {
                localStorage.removeItem('keranjangUser');
            }
        }

        axios
            .get("http://127.0.0.1:8001/api/products", {
                params: {
                    id: this.$route.params.id
                }
            })
            // .then(res => (this.productDetails = res.data.data))
            .then(res => (this.setDataPicture(res.data.data)))
            .catch(err => console.log(err));
    }
}
</script>
