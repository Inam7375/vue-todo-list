<template>
    <button  @click="$emit('toggle')" class="btn" :style="{background: color}">
        {{text}}
    </button>
</template>

<script>
export default{
    name: 'Button',
    props: {
        text: String,
        color: String
    }
}
</script>

