<template>
    <div class="table__row">
      <div class="table__cell table__cell_first-col" :style="{'width': marginForNestedLvl}">
        <NestingControlButton
          @nestingControlButtonClicked="nestingControlHandler"
          :classAppearingModificator="nestingControlButtonClassAppearingModificator"
          class="table__nesting-control-btn"/>
        {{ firstCol }}
      </div>
      <div class="table__cell table__cell_second-col">
        {{ secondCol }}
      </div>
    </div>
</template>

<script>
import NestingControlButton from './UI/NestingControlButton.vue';

export default {
  components: { NestingControlButton },
  props: {
    firstCol: {
      type: String,
      required: true,
    },
    secondCol: {
      type: String,
      required: true,
    },
    hasNestedRows: {
      type: Boolean,
      required: true,
    },
    marginForNestedLvl: {
      type: String,
      default: '35%'
    },
  },
  data() {
    return {
      nestingControlButtonClassAppearingModificator: 'nesting-control-button_visibility_hidden',
    };
  },
  mounted() {
    if (this.hasNestedRows) {
      this.nestingControlButtonClassAppearingModificator = '';
    }
  },
  methods: {
    nestingControlHandler() {
      if (this.nestingControlButtonClassAppearingModificator === 'nesting-control-button_action_expand') {
        this.nestingControlButtonClassAppearingModificator = '';
      } else { 
        this.nestingControlButtonClassAppearingModificator = 'nesting-control-button_action_expand';
      }

      this.$emit('toggleNestingRows')
    }
  },
}
</script>

<style scoped>
.table__row {
  display: flex;
  flex-direction: row;
  width: 100%;
  justify-content: flex-end;
}

.table__cell {
  min-height: 20px;
  border: 1px solid teal;
  padding-left: 10px;
  font-size: 16px;
  line-height: 1.5;
}

.table__cell_first-col {
  width: 35%;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.table__cell_second-col {
  width: 65%;
}

@media screen and (max-width: 820px) {
  .table__cell {
    min-height: 25px;
    font-size: 18px;
    line-height: 1.6;
  }
}
</style>
