<template>
  <div v-if="showLegalObligation && !!getObligations && isBusinessWithNoMaintenanceFilings && !!businessId"
    class="legal-obligation-container"
  >
    <v-card flat class="legal-obligation-section">
      <v-icon color="primary" class="mr-2">mdi-information-outline</v-icon>
      <div>
        <span class="font-weight-bold obligations-title">{{getObligations.title}}</span>
        <span class="obligations-copy">
          You are required by the <em>{{getObligations.act}}</em> {{getObligations.obligationStatement}}
        </span>
        <p class="app-blue cursor-pointer mt-2 mb-0" @click="readMoreFlag = true">
          <span v-if="!readMoreFlag"><u>Read more about your obligations</u></span>
        </p>

        <div v-if="readMoreFlag">
          <div class="obligations-copy pt-2">{{getObligations.subtitle}}</div>
          <div class="pt-2">
            <ul>
              <li v-for="(changes, index) in getObligations.includedChanges" :key="index" class="obligations-copy">
                <span class="font-weight-bold">{{changes.label}}</span> - {{changes.description}}
              </li>
            </ul>
          </div>
          <div class="pt-2">
            <a :href="getObligations.detailInfoURL" target="_blank">Find out more detailed information</a>
            <v-icon color="primary" class="ml-1" small>mdi-open-in-new</v-icon>
          </div>
          <div class="pt-2">
            <span class="app-blue cursor-pointer" @click="readMoreFlag = false"><u>Read less</u></span>
          </div>
        </div>

        <div class="legal-obligation-btn-panel">
          <v-btn id="dismiss-btn" color="primary" @click="showLegalObligation = false" height="25" width="90">
            <span>Dismiss</span>
          </v-btn>
        </div>
      </div>
    </v-card>
  </div>
</template>

<script lang="ts">
import { Component, Mixins } from 'vue-property-decorator'
import { mapGetters } from 'vuex'
import ResourceLookupMixin from '@/mixins/resource-lookup-mixin'

@Component({
  computed: {
    ...mapGetters(['isBusinessWithNoMaintenanceFilings'])
  }
})
export default class LegalObligation extends Mixins(ResourceLookupMixin) {
  readonly isBusinessWithNoMaintenanceFilings!: boolean
  readonly isBComp!: boolean
  private readMoreFlag: boolean = false
  private showLegalObligation: boolean = true

  /** The Business ID string. */
  private get businessId (): string {
    return sessionStorage.getItem('BUSINESS_ID')
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/styles/theme.scss';

.legal-obligation-container {
  display: flex;
  justify-content: center;
  margin-bottom: 1.5rem;
}

.legal-obligation-section {
    display: flex;
    align-items: flex-start;
    padding: 1.2rem;
    font-size: $px-15;
    width: 75%;
}

.obligations-title {
  color: $gray9;
}

.obligations-copy {
  color: $gray7;
}

ul {
  list-style-type: disc;
}

li {
  padding-top: 0.25rem;
}

.legal-obligation-btn-panel {
  float: right;
  margin-top: 1.5rem;
}
</style>
