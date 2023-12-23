<template>
    <div ref="vTags" class="v-tags" :class="classList">
        <component
            v-for="component in elements"
            :key="`${component.component}__${component.id}`"
            :item="component"
            :is="component.component"
        />
    </div>
</template>

<script>
export default {
    name: 'VTags',

    data() {
        return {
            resizeObs: null,
        }
    },

    mounted() {
        this.doCalcVisible();

        this.resizeObs = new ResizeObserver(() => {
            this.doCalcVisible();
        });

        this.resizeObs.observe(this.$refs.vTags);
    },

    beforeDestroy() {
        this.resizeObs.disconnect();
    },

    components: {
        VTag: () => import('@/components/VTag.vue'),
        VDivider: () => import('@/components/VDivider.vue'),
    },

    props: {
        items: {
            type: Array,
            default: () => [],
        },

        alignment: {
            type: String,
            default: 'left',
            validator: (value) => value ? [ 'left', 'space' ].includes(value) : false,
        },
    },

    methods: {
        doCalcVisible() {
            const children = [...this.$el.children];
            const currentRect = this.$el.getBoundingClientRect();

            for (let key in children) {
                const childrenRect = children[key].getBoundingClientRect();
            
                if (childrenRect.right > currentRect.right) {
                    if (!children[key].classList.contains('v-tag')) {
                        return
                    } 

                    children[key].style.opacity = 0;

                    if (key > 0) {
                        children[key - 1].style.opacity = 0;
                    }
                } else {
                    children[key].style.opacity = 1;

                    if (key > 0) {
                        children[key - 1].style.display = 1;
                    }
                }
            }
        },
    },

    computed: {
        classList() {
            return [`_${this.alignment}`];
        },

        elements() {
            const result = [];

            this.items.forEach((item, index) => {
                if (index !== this.items.length - 1) {
                    const id = item.id ? item.id : Math.floor(Math.random() * 100000);

                    result.push({ ...item, component: 'VTag', id: id });
                    result.push({ component: 'VDivider', id: id });
                } else {
                    result.push({ ...item, component: 'VTag' });
                }
            });

            return result;
        },
    },
}
</script>

<style lang="scss" scoped>
    .v-tags {
        width: 100%;
        display: flex;
        column-gap: 8px;
        overflow: hidden;

        &._space {
            justify-content: space-between;
        }

        &._left {
            justify-content: flex-start;
        }
    }
</style>