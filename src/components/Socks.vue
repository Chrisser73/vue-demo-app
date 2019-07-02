<template>

    <div id="socks" class="flex-wrapper">
        <div class="flex-full img-wrapper">
            <h1><strong>{{ msg }}</strong> 😎</h1>
        </div>
        <div class="product-image flex-third">
            <div class="img-wrapper">
                <img :src="mainImage" :alt="alt"/>
            </div>
        </div>

        <div class="product-info flex-third">
            <h3>{{ data.product }}</h3>
            <span v-show="onSale">On sale!</span>
            <p class="info">{{ getSaleStatus }}</p>

            <div class="flex-wrapper">
                <div class="flex-half">
                    <h4>Material</h4>
                    <ul>
                        <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
                    </ul>

                    <div v-if="variants" class="color-choose">
                        <h4>Colors:</h4>
                        <a @mouseover="updateProduct(variant.image)"
                           v-for="variant in variants"
                           :key="variant.variantId"
                           :class="variant.variantColor"
                           :href="'#' + variant.variantColor"
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
				alt: 'Socks',
				inventory: 15,
                inStock: true,
				onSale: true,
				details: ['80% cotton', '20% polyester', 'Gender-neutral'],
				variants: [
					{
						variantId: 2234,
						variantColor: 'green',
                        image: '/assets/socks/vmSocks-green-onWhite.jpg',
					},
					{
						variantId: 2235,
						variantColor: 'blue',
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
				this.inventory -= 1;
				this.checkInventory();
			},
			removeFromCart () {
                this.cart -= 1;
                this.inventory += 1;
				this.checkInventory();
			},
            checkInventory () {
				this.removeIsActive = this.cart > 0 ? true : false;
            },
			updateProduct (image) {
				this.mainImage = image;
            }
		},
        computed: {
			getSaleStatus: function () {
				const invStock = this.inventory;
				if (invStock > 10) {
					this.inStock = true;
					return 'In Stock';
                } else if (invStock <= 10 && invStock > 0){
					this.inStock = true;
					return 'Almost sold out! Just ' + invStock + ' left!'
                } else {
					this.inStock = false;
					return 'Out of Stock'
                }

            }
        }
	};
</script>

<style scoped lang="scss">
    @import 'socks';
</style>
