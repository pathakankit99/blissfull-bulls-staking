<template>
  <div class="center bg-blue-800 shadow-xl p-6">
  <div class="w-full with-title">
    <p class="title">{{ title }}</p>
    <div class="mb-2">Accrued reward: <span class="value">
    {{ reward.accruedReward }}</span></div>
    <div class="mb-2">Paid out reward: <span class="value">{{ reward.paidOutReward }}</span></div>
    <div v-if="parseRewardType(farmReward) === 'variable'">
      <div class="mb-2 w-full bg-indigo-900 my-6 capitalize p-3 text-white">Variable reward:</div>
      <div class="mb-2">
        Last recorded accrued reward per gem:
        <span class="value">{{
          numeral(
            reward.variableRate.lastRecordedAccruedRewardPerRarityPoint.n / 10 ** 15
          ).format('0,0.0')
        }}</span>
      </div>
    </div>
    <div v-else>
      <div class="mb-2 w-full bg-indigo-900 my-6 capitalize p-3 text-white">Fixed reward:</div>
      <div class="mb-2">
        Staking begins: <span class="value">{{ parseDate(reward.fixedRate.beginStakingTs) }}</span>
      </div>
      <div class="mb-2">
        Schedule begins: <span class="value">
        {{ parseDate(reward.fixedRate.beginScheduleTs) }}</span>
      </div>
      <div class="mb-2">
        Last updated: <span class="value">{{ parseDate(reward.fixedRate.lastUpdatedTs) }}</span>
      </div>
      <div class="mb-2">
        Promised duration: <span class="value">{{ reward.fixedRate.promisedDuration }}</span>
      </div>
      <div class="mb-2">Promised schedule:</div>
      <FixedScheduleDisplay
        :key="farmReward"
        class="ml-5"
        :schedule="reward.fixedRate.promisedSchedule"
      />
    </div>
  </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import FixedScheduleDisplay from '@/components/gem-farm/FixedScheduleDisplay.vue';
import { parseDate } from '@/common/util';
import numeral from 'numeral';

export default defineComponent({
  components: { FixedScheduleDisplay },
  props: {
    reward: Object,
    farmReward: Object,
    title: String,
  },
  setup() {
    const parseRewardType = (reward: any): string => {
      //returns "variable" or "fixed"
      return Object.keys(reward.rewardType)[0];
    };

    return {
      parseRewardType,
      parseDate,
      numeral,
    };
  },
});
</script>

<style scoped></style>
