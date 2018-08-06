<template>
    <div
        v-if="isActive"
        :class="{ 'disabled': isDisabled }">

        <slot/>
    </div>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            required: true
        },
        active: {
            type: [ Boolean, String ],
            default: false
        },
        route: {
            type: [ Boolean, String ],
            default: false
        },
        disabled: {
            type: [ Boolean, String ],
            default: false
        }
    },

    /**
     * Data.
     *
     * @return {object}
     */
    data() {
        return {
            isActive: this.active,
            isDisabled: this.disabled
        }
    },

    computed: {
        /**
         * Index.
         *
         * @return {number}
         */
        index() {
            return this.$parent.tabList.indexOf(this);
        }
    },

    watch: {
        /**
         * Active tab index.
         *
         * @param {boolean} index
         */
        '$parent.activeTabIndex'(index) {
            this.isActive = this.index === index;
        },
        /**
         * Disabled.
         */
        disabled() {
            this.isDisabled = this.disabled;
        }
    },

    /**
     * Created.
     */
    created() {
        this.$parent.tabList.push(this);
    },
}
</script>
