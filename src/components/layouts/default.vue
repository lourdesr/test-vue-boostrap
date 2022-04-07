<template>
    <div id="layout">
        <topbar></topbar>
        <div class="main-content">
            <slot></slot>
        </div>
        <footer-nav></footer-nav>
    </div>
</template>
<script>
import FooterNav from '@/components/partials/Footer.vue';
import topbar from '@/components/partials/Topbar.vue';
export default {
    name: 'default-layout',
    components: {
        FooterNav,
        topbar
    }
}
</script>