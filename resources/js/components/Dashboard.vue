<template>
    <div class="container">
        <div id="app">
            Form: <input type="text" v-model="orange">
            To: <input type="text" v-model="destination">
            <iframe width="100%" height="500px" src=""></iframe>
        </div>
    </div>
</template>

<script>
    
        export default {
             el:'#app',
            data:{
                orange:'Giza',
                destination:'egypt',
                url:"VUE_APP_GOOGLE_MAPS_API_KEY=ABcdEfGhIjklmNOpqrsTUvWXyzAbcD1EfGhiJKl"
            },
            methods:{
                src:function(){
                    return this.url="&orange"+orange+"&destination="+this.destination;
                }
            },
        mounted() {
            console.log('Component mounted.')
        }
    }
    
</script>
