<template>
  <div v-if="filing" class="filed-label d-inline">
    <template v-if="filing.isTypeStaff">
      <span>Filed by {{filing.submitter}} on <DateTooltip :date="filing.submittedDate" /></span>
    </template>

    <template v-else>
      <span> (filed by {{filing.submitter}} on <DateTooltip :date="filing.submittedDate" />)</span>
      <span class="vert-pipe" />
      <span>EFFECTIVE as of <DateTooltip :date="filing.effectiveDate" /></span>
    </template>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'
import { DateTooltip } from '@/components/common'
import { HistoryItemIF } from '@/interfaces'

@Component({
  components: { DateTooltip }
})
export default class FiledLabel extends Vue {
  @Prop({ required: true })
  readonly filing: HistoryItemIF
}
</script>
