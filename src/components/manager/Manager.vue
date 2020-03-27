<template>
    <div class="fm-content d-flex flex-column">
        <disk-list v-bind:manager="manager"></disk-list>
        <breadcrumb v-bind:manager="manager"></breadcrumb>
        <div class="fm-content-body">
            <component :is="tableView" v-if="viewType === 'table'" v-bind:manager="manager"></component>
            <component :is="gridView" v-else v-bind:manager="manager"></component>
        </div>
    </div>
</template>

<script>
// Components
import DiskList from './DiskList.vue';
import Breadcrumb from './Breadcrumb.vue';
import TableView from './TableView.vue';
import GridView from './GridView.vue';

export default {
  name: 'Manager',
  components: {
    DiskList,
    Breadcrumb,
    TableView,
    GridView,
  },
  props: {
    manager: { type: String, required: true },
  },
  computed: {
    /**
     * view type - grid or table
     * @returns {default.computed.viewType|(function())|string}
     */
    viewType() {
      return this.$store.state.fm[this.manager].viewType;
    },
    /**
     * Return default or custom grid view component
     */
    tableView() {
      return this.$store.state.fm.settings.customTableView ? this.$store.state.fm.settings.customTableView : TableView;
    },
    /**
     * Return default or custom grid view component
     */
    gridView() {
      return this.$store.state.fm.settings.customGridView ? this.$store.state.fm.settings.customGridView : customGridView;
    }
  },
};
</script>

<style lang="scss">
    .fm-content {
        height: 100%;
        padding-left: 1rem;

        .fm-content-body {
            overflow: auto;
        }
    }
</style>
