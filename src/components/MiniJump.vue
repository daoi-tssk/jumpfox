<template>
  <div id="MiniJump">
    <Environment/>
    <MainRole/>
  </div>
</template>

<script>
import Environment from './environment/Environment'
import MainRole from './mainrole/MainRole'

export default {
  name: 'MiniJump',
  components: {
    Environment,
    MainRole,
  }
}
</script>

<style scoped>

</style>