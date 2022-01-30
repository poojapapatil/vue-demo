<template>
    <div id="app" class="main">
        <div class="heading">
            <h1>{{heading}}</h1>
        </div>
        <div class="body">
            <div class="product-image">
                <img :src="image" height="100px" width="100px"/>
            </div>
            <div class="product-detail">
                <h3>{{title}}</h3>
                <p v-if="!inStock">In Stock</p>
                <!--<p v-else-if="inventory < 10 && inventory > 0">Almost Sold Out</p>-->
                <p v-else>Out of stock</p>
                <ul>
                    <li v-for="detail in details">{{detail}}</li>
                </ul>
                <div class="product-color-wrapper">
                    <div v-for="(v, index) in variants":key="v.variantId"
                         class="product-color"
                         :style="{backgroundColor:v.variantColor}"
                         @mouseover="updateProduct(index)">
                    </div>
                </div>
                <button v-on:click="addToCart" :disabled="!inStock" class="add-to-cart-btn">Add to Cart</button>
                <div>Cart Items : ({{cart}})</div>
            </div>
        </div>

    </div>
</template>
<script>
    import './home.css';
    export default {
        el:'#app',
        name: 'Home',
        props: {
            msg: String
        },
        data: () => {
            return {
                heading:'Shopping Cart demo',
                product:'Socks',
                selectedVariant:0,
                inventory:100,
                details:["80%  Cotton","20% Polyester"],
                variants:[
                    {
                        variantId:1,
                        variantColor:"black",
                        variantImage:require('../assets/BlackSocks.jpg'),
                        variantQty:10,
                    },
                    {
                        variantId:2,
                        variantColor:"purple",
                        variantImage:require('../assets/PurpleSocks.jpg'),
                        variantQty:0
                    }
                ],
                cart: 0,
            }
        },
        methods:{
            addToCart(){
               this.cart+=1;
            },
            updateProduct(variantId){
                this.selectedVariant= variantId
            }
        },
        computed:{
            title(){
                return 'Vue '+ this.product;
            },
            image(){
                return this.variants[this.selectedVariant].variantImage;
            },
            inStock(){
                return this.variants[this.selectedVariant].variantQty;
            }
        }
    }
</script>