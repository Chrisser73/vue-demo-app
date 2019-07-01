<template>
    <div id="app">

        <div class="nav-bar"></div>

        <div class="img-wrapper"><img alt="Vue logo" src="./assets/logo.png"></div>
        <Socks
                msg="My Cool Shop"
                :data="{
                    product:'Socks',
                    url: 'https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg',
                }"
        />
    </div>
</template>

<script>
	import Socks from './components/Socks.vue';

	export default {
		name: 'app',
		components: {
			Socks
		}
	};
</script>

<style>
    @import './main/normalize.css';
    @import 'app.scss';
</style>
