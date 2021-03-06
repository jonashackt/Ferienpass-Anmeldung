<template>
  <label class="checkbox">
    <input
      class="checkbox__control visually-hidden"
      type="checkbox"
      :name="toIdentifier(params.label)"
      :required="params.required"
      @change="onChecked"
    >

    <span class="checkbox__tick"></span>

    <span class="checkbox__label">
      <template v-if="params.date && params.org">
        <span class="offer">
          <span class="offer__title">{{ params.label }}</span>
          <span class="offer__date">{{ params.date }}</span>
          <span class="offer__org">{{ params.org }}</span>
        </span>
      </template>
      <template v-else>
        {{ params.label }}
      </template>
    </span>
  </label>
</template>

<script>
export default {
  name: 'Checkbox',
  props: ['params'],
  methods: {
    onChecked(event) {
      this.$emit('change', event.target.checked);
    }
  }
};
</script>

<style scoped>
.checkbox {
  display: flex;
  align-items: center;
  position: relative;
  margin-bottom: 0.75rem;
}

.checkbox__label {
  padding-right: 24px;
  padding-left: 8px;
}

.checkbox__tick {
  flex-shrink: 0;
  position: relative;
  width: 1.5rem;
  height: 1.5rem;
  margin: 2px;
  background-color: #fff;
  border-radius: 8px;
  border: 2px solid #000;
}

/*
We explicitly set the height of the control to be as tall as its next parent context.
This is necessary for when one navigates to a control outside the current viewport.
Then, current scrolling distance would adjust as much as to fit in the full control.
Making it 100% the height of its parenting context should cover the whole component,
not only the control. The reason this is problematic is the control being visually
hidden, thus only having a dimension of 1 by 1 pixels. In other words, without this,
the componente would only become partially visible.
*/
.checkbox__control {
  position: absolute !important;
  top: 0 !important;
  height: 100% !important;
  outline: none;
}

.checkbox__control:focus ~ .checkbox__tick {
  /* box-shadow: 0 0 0 2px #fff, 0 0 0 4px cornflowerblue; */
  box-shadow: 0 0 0 2px cornflowerblue;
}

.checkbox__control:checked ~ .checkbox__tick::before {
  content: '\2713';
  width: 100%;
  height: 100%;
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
}

.offer {
  display: flex;
  flex-direction: column;
}

.offer__date {
  order: -1;
  font-size: 0.75em;
}

.offer__title {
  font-weight: bold;
}
</style>
