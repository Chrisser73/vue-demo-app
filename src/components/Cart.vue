<template>
    <div id="cart" class="flex-half">
        <div class="cart">
            <p>Cart({{ data.cart }})</p>
        </div>
    </div>


</template>

<script>
	export default {
		name: 'Cart',
		props: {
			data: {
				card: Number
			}

		}
	};
</script>

<style scoped lang="scss">
    @import 'cart';
</style>