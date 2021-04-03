<template>

<header v-show="showHeader">
    <h3>{{text}}</h3>
    <Button @toggle="$emit('toggle')" :text="showForm ? 'Close' : 'Add Form'" :color="showForm ? 'red' : 'green'"/>
</header>

</template>


<script>
import Button from './Button'
export default{
    name: 'Header',
    components: {
        Button
    },
    emits:['toggle'],
    props: {
        'text': String,
        'showForm': Boolean
    },
    computed : {
        showHeader(){
            if(this.$route.path === '/'){
                return true  
            } else {
                return false
            }     
        }
    }
}
</script>

<style>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 2em;
}
</style>

