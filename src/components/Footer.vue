<template>
    <div>
        <h4>Copyright &copy; 2021</h4>
        <router-link :to="toggleLink ? '/about' : '/'">{{text}}</router-link>
    </div>
</template>

<script>
export default{
    name: 'Footer',
    data() {
        return{
            text: 'About',
            link: ''
        }
    },
    computed: {
        toggleLink(){
            if(this.$route.path === '/'){
                this.text = 'About'
                return true
            } else {
                this.text = 'Home'
                return false
            }
        }
    }
}
</script>

<style scoped> 
    a {
        color: #333;
    }
    div {
        margin-top: 1.5em;
        text-align: center;
    }
</style>