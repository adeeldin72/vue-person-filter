<template>
    <div class="card">
        <slot></slot>
    </div>
</template>

<script>
export default {
    props: [''],
}
</script>

<style>
    .card {
        border-radius: 12px;
        box-shadow: 0 1px 8px rgba(0, 0, 0, 0.25);
        overflow: hidden;    
    }

</style>