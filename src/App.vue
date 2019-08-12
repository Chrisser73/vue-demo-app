<template>
    <div id="app">

        <div class="nav-bar"></div>
        <div class="img-wrapper"><img alt="Vue logo" src="../public/assets/logo.png"></div>

        <Product
            msg="My Cool Shop"
            :premium=premium
            :productData="{
                brand: 'Vue Mastery',
                product:'Socks',

            }"
        />

    </div>
</template>

<script>
	import Product from './components/Product.vue';

	export default {
		name: 'app',
		components: {
			Product
		},
        data() {
			return {
				premium: false
            }
        }

	};
</script>

<style lang="scss">
    @import './main/normalize.css';
    @import './main/main.scss';
</style>

<style scoped lang="scss">
    @import './app.scss';
</style>