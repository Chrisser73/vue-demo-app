<template>
    <div id="app">

        <Menu />

        <div class="img-wrapper vue-logo"><img alt="Vue logo" src="../public/assets/vue-intro-logo.svg"></div>

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
	import Menu from './components/Menu.vue';

	export default {
		name: 'app',
		components: {
			Product,
            Menu
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