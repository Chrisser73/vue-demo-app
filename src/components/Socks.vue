<template>

    <div id="socks" class="flex-wrapper">
        <div class="flex-full img-wrapper">
            <h1><strong>{{ msg }}</strong> 😎</h1>
        </div>
        <div class="product-image flex-half">
            <div class="img-wrapper">
                <img :src="data.url" :alt="alt"/>
            </div>
        </div>

        <div class="product-info flex-half">
            <h3>{{ data.product }}</h3>
            <span v-show="onSale">On sale!</span>

            <p v-if="inventory > 10" style="color: green">In Stock</p>
            <p v-else-if="inventory <= 10 && inventory > 0">Almost sold out!</p>
            <p v-else>Out of Stock</p>

            <p>{{ getSaleStatus }}</p>

            <div class="flex-wrapper">
                <div class="flex-half">
                    <h4>Material</h4>
                    <ul>
                        <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
                    </ul>


                    <div v-if="variants" class="color-choose">
                        <h4>Colors:</h4>
                        <a v-for="variant in variants" :key="variant.variantId" href="" :class="variant.variantColor"></a>
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
                    <div class="flex-half">
                        <button v-on:click="addToCart">Add to Cart</button>
                    </div>
                    <div class="flex-half">
                        <div class="cart">
                            <p>Cart({{ cart }})</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
	export default {
		name: 'Socks',
		props: {
			msg: String,
			data: {
				product: String,
				url: String
			}
		},
		data() {
			return {
				alt: 'Socks',
				inventory: '100',
				onSale: true,
				details: ['80% cotton', '20% polyester', 'Gender-neutral'],
				variants: [
					{
						variantId: 2234,
						variantColor: 'green'
					},
					{
						variantId: 2235,
						variantColor: 'blue'
					}
				],
				sizes: ['XS', 'S', 'M', 'L', 'XL', 'XXL'],
				cart: 0
			};
		},
		methods: {
			addToCart: function () {
				this.cart += 1;
			}
		},
        computed: {
			getSaleStatus: function (){
				if (this.inventory > 10) {
					return 'In Stock';
                } else if (this.inventory <= 10 && this.inventory > 0){
					return 'Almost sold out!'
                } else {
					return 'Out of Stock'
                }

            }
        }
	};
</script>

<style scoped>
    @import 'socks.scss';
</style>
