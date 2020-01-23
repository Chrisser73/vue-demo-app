<template>

    <div id="cart" class="flex-half">
        <div v-if="cartData.premium" class="premium"><img class="icon mr-1" src="../../public/assets/diamond.svg"/> Premium User</div>
        <div class="cart mb-1">
            <p>Quantity ({{ cartData.cart }})</p>
            <hr>
            <div v-if="shippingPrice">
                <p>Shipping: ${{ shippingPrice }}</p>
                <hr>
            </div>
            <p><strong>TOTAL:</strong> {{priceTotal}}</p>
        </div>
        <div class="flex-full">
                <div class="pull-right">
                    <button
                        v-on:click="checkoutBtn"
                        :disabled="checkoutBtn"
                        :class="{ disabledButton: !checkoutBtn}"
                    >Add to Cart
                    </button>
                </div>
        </div>
    </div>

</template>

<script>
	export default {
		name: 'Cart',
		props: {
			cartData: {
				card: Number,
				premium: Boolean,
				priceTotal: Number,
			}
		},
		data() {
			return {
				shippingCosts: 0,
			}
		},
		computed: {
			shippingPrice() {
				if(!this.cartData.premium){
					// eslint-disable-next-line
                    this.shippingCosts = 5.99
                    return this.shippingCosts;
                } else {
					return this.shippingCosts;
                }
			},
            checkoutBtn() {
				return this.cartData.cart > 0;
            },
			priceTotal() {
				let formatter = new Intl.NumberFormat('en-US', {
					style: 'currency',
					currency: 'USD',
				});

				return formatter.format(this.cartData.priceTotal + this.shippingPrice);
            }
        }
	};
</script>

<style scoped lang="scss">
    @import 'cart';
</style>