<template>
  <p>
    Enter grades (0-100) for the modules you have completed.
  </p>

  <div class="classes-wrapper">
    <Classes />
  </div>
</template>

<script>
import Classes from './Classes.vue'

export default {
  name: 'Calculator',
  components: {
    Classes
  }
}
</script>

<style scoped>
p {
  margin: 16px;
}
.classes-wrapper {
  width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
}

@media screen and (max-width: 600px) {
  .classes-wrapper {
    overflow: scroll;
    flex-direction: unset;
    align-items: unset;
  }
}
</style>
