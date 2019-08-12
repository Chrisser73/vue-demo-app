<template>

    <div id="socks" class="flex-wrapper">
        <div class="flex-full img-wrapper">
            <h1><strong>{{ msg }}</strong> 😎</h1>
        </div>
        <div class="product-image flex-third">
            <div class="img-wrapper">
                <span class="saleBanner" v-show="onSale">On sale!</span>
                <img :src="this.image" :alt="alt"/>
            </div>
        </div>

        <div class="product-info flex-third">
            <h3>{{ title }}</h3>
            <p class="info" :class="{outOfStock: !inStock, almostSoldOut: inStock <= 10 && inStock > 0}">{{ getSaleStatus }}</p>

            <div class="flex-wrapper">
                <div class="flex-half">
                    <h4>Material</h4>
                    <ul>
                        <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
                    </ul>

                    <div v-if="variants" class="color-choose">
                        <h4>Colors:</h4>

                        <a v-for="(variant, index) in variants"
                           :key="variant.variantId"
                           :class="variant.variantColor"
                           :href="'?' + updateHref(index)"
                           @mouseover="updateProduct(index)"
                        ></a>

                    </div>
                </div>

                <div class="flex-half">
                    <div v-if="sizes.length > 0">
                        <h4>Sizes</h4>
                        <ul>
                            <li v-for="(size, index) in sizes" :key="index">{{ size }}</li>
                        </ul>
                    </div>
                </div>
            </div>
            <div class="flex-full">
                <hr/>
                <div class="flex-wrapper">
                    <div class="flex-half pull-right">
                        <button
                            v-on:click="removeFromCart"
                            :disabled="!removeIsActive"
                            :class="{ disabledButton: !removeIsActive}"
                        >Remove from Cart</button>
                    </div>
                    <div class="flex-half pull-right">
                        <button
                            v-on:click="addToCart"
                            :disabled="!inStock"
                            :class="{ disabledButton: !inStock}"
                        >Add to Cart</button>
                    </div>
                </div>
            </div>
        </div>

        <template>
            <Cart
                :data="{
                    cart
                }"
            />
        </template>
    </div>
</template>

<script>
	import Cart from './Cart.vue';

	export default {
		name: 'Socks',
		props: {
			msg: String,
			data: {
				product: String
			}
		},
		components: {
			Cart
		},
		data() {
			return {
				mainImage: '/assets/socks/vmSocks-green-onWhite.jpg',
                selectedVariant: 0,
				alt: 'Socks',
				details: ['80% cotton', '20% polyester', 'Gender-neutral'],
				variants: [
					{
						variantId: 2234,
						variantColor: 'green',
						onSale: false,
						inventory: 15,
                        image: '/assets/socks/vmSocks-green-onWhite.jpg',
					},
					{
						variantId: 2235,
						variantColor: 'blue',
						onSale: true,
						inventory: 7,
						image: '/assets/socks/vmSocks-blue-onWhite.jpg',
					}
				],
				sizes: ['XS', 'S', 'M', 'L', 'XL', 'XXL'],
				cart: 0,
				removeIsActive: false,
			};
		},
		methods: {
			addToCart () {
				this.cart += 1;
				this.variants[this.selectedVariant].inventory -= 1;
				this.checkInventory();
			},
			removeFromCart () {
                this.cart -= 1;
				this.variants[this.selectedVariant].inventory += 1;
				this.checkInventory();
			},
            checkInventory () {
				this.removeIsActive = this.cart > 0 ? true : false;
            },
			updateHref(paramColor){
				var urlParam = 'color' + '=' + paramColor;
                return urlParam;
            },
			updateProduct (index) {
                this.selectedVariant = index;
			}
		},
		beforeMount(){
			const urlParams = new URLSearchParams(window.location.search);
			const colorVar = urlParams.get('color');

			console.log(colorVar);
		},
        computed: {
			title() {
				return this.data.brand + ' ' + this.data.product
            },
            image() {
                return this.variants[this.selectedVariant].image
            },
			inStock() {
				return this.variants[this.selectedVariant].inventory
            },
			onSale(){
				return this.variants[this.selectedVariant].onSale
            },
			getSaleStatus: function () {
				if (this.inStock > 10) {
					return 'In Stock';
                } else if (this.inStock <= 10 && this.inStock > 0){
					return 'Almost sold out! Just ' + this.inStock + ' left!'
                } else {
					return 'Out of Stock'
                }

            }
        }
	};
</script>

<style scoped lang="scss">
    @import 'socks';
</style>
