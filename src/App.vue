<template>
    <VApp>
        <div class="container">
            <VTags
                :items="tags"
                alignment="left"
            />
        </div>

        <div class="container">
            <VTags
                :items="tags"
                alignment="space"
            />
        </div>

        <div class="container container--small">
            <VTags
                :items="tags"
                alignment="left"
            />
        </div>

        <div class="container container--small">
            <VTags
                :items="tags"
                alignment="space"
            />
        </div>
    </VApp>
</template>

<script>
import VTags from '@/components/VTags.vue';

export default {
    name: 'App',

    components: {
        VTags,
    },
    
    data() {
        return {
            tags: [
                {
                    id: 1,
                    icon: 'mdi-star',
                    text: '4,3',
                },
                {
                    id: 2,
                    text: 'Фридландские ворота',
                },
                {
                    id: 3,
                    text: '1,2 км от вас',
                },
            ],
        };
    },
};
</script>

<style lang="scss" scoped>
    .container {
        width: 100%;
        padding: 32px 16px;

        &--small {
            width: 50%;
        }
    }
</style>
