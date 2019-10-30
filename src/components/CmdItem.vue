<template>
  <div>
    <span v-if="hovered">
      ▶
    </span>

    {{ item.label }}
    <CmdWindow
      v-if="selected"
      :items="item.children"
      @close="$emit('close')"
    ></CmdWindow>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'CmdItem',
  components: {
    CmdWindow: () => import('@/components/CmdWindow.vue')
  },
  props: {
    item: {
      type: Object,
      required: true
    },
    selected: {
      type: Boolean,
      required: true
    },
    hovered: {
      type: Boolean,
      required: true
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}

a {
  color: #42b983;
}
</style>
