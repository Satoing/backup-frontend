<template>
  <button @click="flag=true">备份</button>
  <button @click="flag=false">还原</button>
  <div v-if="flag">
    <Backup></Backup>
  </div>
  <div v-if="!flag">
    <Restore></Restore>
  </div>
</template>

<script>
import Backup from './components/backup.vue'
import Restore from './components/restore.vue'

export default {
  data() {
    return {
      flag: true,
    }
  },
  components: {
    Backup,
    Restore
  }
};
</script>