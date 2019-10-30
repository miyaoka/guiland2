<template>
  <ul>
    <CmdItem
      v-for="(item, i) in items"
      :key="i"
      :item="item"
      :hovered="cursorIndex === i"
      :selected="selectedIndex === i"
      @close="onCloseItem"
    ></CmdItem>
  </ul>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'CmdWindow',
  components: {
    CmdItem: () => import('@/components/CmdItem.vue')
  },
  data() {
    return {
      cursorIndex: 0,
      selectedIndex: -1
    }
  },
  props: {
    title: {
      type: String,
      required: false,
      default: ''
    },
    items: {
      type: Array,
      required: false,
      default: () => []
    }
  },
  mounted() {},
  destroyed() {},
  watch: {
    selectedIndex: {
      immediate: true,
      handler(val) {
        if (val < 0) {
          document.addEventListener('keydown', this.onKeydown)
        } else {
          document.removeEventListener('keydown', this.onKeydown)
        }
      }
    }
  },
  methods: {
    onKeydown(e: KeyboardEvent) {
      switch (e.key) {
        case 'Escape':
          this.unselect()
          break
        case 'ArrowUp':
          this.moveCursor(-1)
          break
        case 'ArrowDown':
          this.moveCursor(1)
          break
        case 'Enter':
          this.select()
          break
      }
    },
    onCloseItem() {
      this.selectedIndex = -1
    },
    unselect() {
      this.$emit('close')
    },
    select() {
      const item = this.items[this.cursorIndex]

      if (item.children) {
        this.selectedIndex = this.cursorIndex
        return
      }
      item.cmd && item.cmd()
    },
    moveCursor(diff: number) {
      const len = this.items.length
      this.cursorIndex = (((this.cursorIndex + diff) % len) + len) % len
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  border: 4px solid #000;
  border-radius: 8px;
  margin: 10px;
}

a {
  color: #42b983;
}
</style>
