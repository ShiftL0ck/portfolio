<template lang="pug">
  .query-tooltip(
    v-if="show"
    :class="{'success': type === 'success', 'error': type === 'error'}"
  )
    span.query-tooltip__text {{text}}
    button(
      type="button"
      @click="CLOSE_TOOLTIP"
    ).btn.btn--close-tooltip
</template>

<script>
import { mapState, mapMutations } from "vuex";

export default {
  data() {
    return {
      timeout: 3000
    }
  },
  computed: {
    ...mapState("tooltip", {
      show: state => state.show,
      type: state => state.type,
      text: state => state.text
    })
  },
  methods: {
    ...mapMutations("tooltip", ["CLOSE_TOOLTIP"])
  },
  updated() {
    setTimeout(this["CLOSE_TOOLTIP"], this.timeout);
  }
};
</script>

<style lang="postcss" scoped>
.query-tooltip {
  position: fixed;
  top: 55%;
  left: 50%;
  transform: translateX(-50%);
  padding: 60px 60px;
  z-index: 1000;
  color: #fff;
  display: flex;
  align-items: center;
  border-radius: 10px;

  &.success {
    background: rgba(green, 0.6);
  }

  &.error {
    background: rgba(red, 0.85);
  }
}

.query-tooltip__text {
  margin-right: 50px;
}
</style>
