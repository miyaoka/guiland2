<template>
  <div class="home">
    <cmd-window :items="items" />
  </div>
</template>

<script>
import CmdWindow from '@/components/CmdWindow.vue'

export default {
  name: 'home',
  data() {
    return {
      items: [
        {
          label: 'はなす',
          cmd: () => {
            alert('こんにちは')
          }
        },
        {
          label: 'しらべる',
          children: [
            {
              label: 'きた',
              children: [
                {
                  label: 'みぎ'
                },
                {
                  label: 'ひだり'
                },
                {
                  label: 'まんなか'
                }
              ]
            },
            { label: 'ひがし' },
            { label: 'みなみ' }
          ]
        },
        {
          label: 'どうぐ',
          children: [
            { label: 'やくそう' },
            { label: 'やくそう' },
            { label: 'ふく' },
            { label: 'やくそう' },
            { label: 'ごはん' },
            { label: 'やくそう' }
          ]
        }
      ]
    }
  },
  components: {
    CmdWindow
  }
}
</script>
