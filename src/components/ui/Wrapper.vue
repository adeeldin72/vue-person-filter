<template>
    <div class="wrapper">
        <slot></slot>
    </div>
</template>

<script>
export default {
    props: [''],
}
</script>

<style>
    .wrapper {
        max-width: 1750px;
        margin: 0 auto;
    }
</style>