<template>
  <b-card header-tag="header" no-body>
    <template v-slot:header>
      <div
        @click="open = !open"
        class="block-header d-flex justify-content-between font-size-14 font-w600 cursor"
      >
        <span class="my-1" :class="darkMode ? 'text-dark' : 'text-light'">
          <font-awesome-icon
            v-if="headerIcon"
            :icon="headerIcon"
            class="mr-1"
            :class="darkMode ? 'text-white' : 'text-primary'"
          />
          {{ title }}
        </span>

        <font-awesome-icon
          :icon="open ? 'caret-up' : 'caret-down'"
          :class="darkMode ? 'text-white' : 'text-primary'"
        />
      </div>
    </template>

    <b-collapse id="collapse-block" v-model="open">
      <slot></slot>
    </b-collapse>
  </b-card>
</template>
<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { vxm } from "@/store/";

@Component({
  components: {}
})
export default class CollapsableBlock extends Vue {
  @Prop() title!: string;
  @Prop({ default: "" }) headerIcon!: string;

  open = false;

  get darkMode() {
    return vxm.general.darkMode;
  }
}
</script>

<style scoped lang="scss">
@import "../../assets/_scss/custom/_variables";
.card {
  border: 1px solid $block-header-gray !important;
  border-radius: 8px !important;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.04),
    0 1px 2px 0 rgba(15, 89, 209, 0.08) !important;
  background-color: $block-bg-blue !important;
}
.card-header {
  padding: 0 !important;
  margin-bottom: 0 !important;
  background-color: $block-header-gray !important;
  border-bottom: none !important;
  border-radius: 8px 8px !important;
}
</style>
