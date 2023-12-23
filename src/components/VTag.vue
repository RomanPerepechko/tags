<template>
    <div class="v-tag">
        <VIcon
            v-if="item.icon"
            class="v-tag__icon"
            small
        >
            {{ item.icon }}
        </VIcon>
        
        <div class="v-tag__text">
            {{ item.text }}
        </div>
    </div>
</template>

<script>
import VIcon from 'vuetify';

export default {
    name: 'VTag',

    components: {
        VIcon,
    },

    props: {
        item: {
            type: Object,
            default: () => ({}),
        },
    },
}
</script>

<style lang="scss" scoped>
    .v-tag {
        display: flex;
        column-gap: 4px;
        white-space: nowrap;
        opacity: 0;
        transition: opacity .3s ease;
    }
</style>