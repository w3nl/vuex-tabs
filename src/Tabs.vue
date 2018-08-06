<template>
    <div>
        <ul>
            <li
                v-for="(tab, index) in tabList"

                :key="index"
                :class="{active: isActive(index), disabled: tab.disabled}"

                @click="select(index)"
            >
                {{ tab.title }}
            </li>
        </ul>
        <div class="tab-content">
            <slot/>
        </div>
    </div>
</template>

<script>
export default {
    /**
     * Data.
     *
     * @return {object}
     */
    data() {
        return {
            tabList: [],
            activeTabIndex: 0
        }
    },

    /**
     * Mounted.
     */
    mounted() {
        this.activeTabIndex = this.getInitialActiveTab();
        this.select(this.activeTabIndex);

        this.$root.$on('select-tab', index => this.select(index));
    },

    methods: {
        /**
         * Is active.
         *
         * @param {number} index
         *
         * @return {boolean}
         */
        isActive(index) {
            return this.activeTabIndex === index;
        },

        /**
         * Select.
         *
         * @param {number} index
         */
        select(index) {
            const tab = this.tabList[index];

            if (!tab.isDisabled) {
                this.activeTabIndex = index;
            }

            this.$router.push({ name: tab.route });
        },

        /**
         * Get initial active tab.
         *
         * @return {number}
         */
        getInitialActiveTab() {
            const routeName = this.$route.name;
            const index = this.tabList.findIndex(tab => tab.active);
            const pageIndex = this.tabList.findIndex(tab => tab.route == routeName);

            if (index === -1) {
                return 0;
            }

            if (pageIndex > -1) {
                return pageIndex;
            }

            return index;
        }
    }
}
</script>
