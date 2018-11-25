<template>
  <div class="vue-infinite-grid" :class="customCssClass" :id="gridId">
    <slot/>
  </div>
</template>
<script>
  import InfiniteGrid, {GridLayout, JustifiedLayout, FrameLayout, SquareLayout, PackingLayout} from "@egjs/infinitegrid"
  export default {
    name: 'vue-infinite-grid',
    props: {
      customCssClass: {
        type: [String, Array]
      },
      layout: {
        type: String
      },
      layoutConfig: {
        type: Object
      },
      options: {
        type: Object
      },
    },
    data () {
      return {
        id: Math.random().toString(36).substr(2, 10),
        infiniteGrid: null
      }
    },
    mounted () {
      var vm = this;
      vm.infiniteGrid = new InfiniteGrid(vm.$el, vm.options || {});

      this.$nextTick(() => {
        vm.infiniteGrid.setLayout(this.gridType || JustifiedLayout, vm.layoutConfig || []);
      })
    },
    computed: {
      gridId () {
        return `grid_${this.id}`
      },
      gridType () {
        switch (this.layout) {
          case 'JustifiedLayout':
            return JustifiedLayout
          case 'FrameLayout':
            return FrameLayout
          case 'SquareLayout':
            return SquareLayout
          case 'PackingLayout':
            return PackingLayout
          case 'GridLayout':
            return GridLayout
        }
      }
    }
  }
</script>
