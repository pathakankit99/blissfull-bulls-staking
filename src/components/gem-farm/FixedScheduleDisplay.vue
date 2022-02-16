<template>
  <div>
    <div class="mb-2">Base rate: <span class="value">{{ schedule.baseRate }} tokens/gem/s</span></div>
    <div class="mb-2" v-if="schedule.tier1">
      T1 reward rate:
      <span class="value">{{ schedule.tier1.rewardRate }} tokens/gem/s</span>
    </div>
    <div class="mb-2" v-if="schedule.tier1">
      T1 required tenure:
      <span class="value">{{ schedule.tier1.requiredTenure }} sec</span>
    </div>
    <!--tier 2-->
    <div class="mb-2" v-if="schedule.tier2">
      T2 reward rate:
     <span class="value"> {{ schedule.tier2.rewardRate }} tokens/gem/s</span>
    </div>
    <div class="mb-2" v-if="schedule.tier2">
      T2 required tenure:
     <span class="value"> {{ schedule.tier2.requiredTenure }} sec</span>
    </div>
    <!--tier 3-->
    <div class="mb-2" v-if="schedule.tier3">
      T3 reward rate:
      <span class="value">{{ schedule.tier3.rewardRate }} tokens/gem/s</span>
    </div>
    <div class="mb-2" v-if="schedule.tier3">
      T3 required tenure:
      <span class="value">{{ schedule.tier3.requiredTenure }} sec</span>
    </div>
    <div class="mb-2">
      Denominator:
      <span class="value">{{ schedule.denominator }}</span>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
  props: {
    schedule: Object,
  },
  setup() {
    return {};
  },
});
</script>

<style scoped></style>
