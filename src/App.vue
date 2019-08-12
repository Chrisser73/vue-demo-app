<template>
    <div id="app">

        <div class="nav-bar"></div>

        <div class="img-wrapper"><img alt="Vue logo" src="../public/assets/logo.png"></div>
        <Socks
                msg="My Cool Shop"
                :data="{
                    product:'Socks',
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

<style lang="scss">
    @import './main/normalize.css';
    @import './main/main.scss';
</style>

<style scoped lang="scss">
    @import './app.scss';
</style>