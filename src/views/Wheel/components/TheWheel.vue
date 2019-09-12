<template>
    <svg 
        class="the-wheel"
        :class="{ 'kick-in' : start }" 
        version="1.1" 
        baseProfile="full" 
        xmlns="http://www.w3.org/2000/svg">
        <circle class="the-wheel-circle" cx="25" cy="25" r="25"  />
        <line class="the-wheel-line" x1="25" y1="25" x2="25" y2="50" />
    </svg>
</template>

<script>
export default {
    props: {
        start: {
            type: Boolean,
            default: false
        }
    }
}
</script>