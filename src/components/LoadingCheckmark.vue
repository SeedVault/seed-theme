<template>
  <div class="text-center" v-if="visible">
    <div v-bind:class="[{ 'load-complete': !loading }, 'circle-loader']">
      <div class="checkmark draw" v-show="showCheckmark"></div>
      <slot name="icons"></slot>
    </div>
    <slot name="messages"></slot>
  </div>
</template>

<script>
export default {
  name: 'LoadingCheckmark',
  props: ['visible', 'loading', 'showCheckmark'],
};
</script>

<style lang="scss" scoped>
@import "../scss/colors";
$check-loader-size: 6em;
$check-height: $check-loader-size/2;
$check-width: $check-height/2;
$check-left: ($check-loader-size/6 - ($check-loader-size / 14) + $check-loader-size/12);
$check-thickness: 4px;
$check-color: $primary;


.circle-loader {
  margin-bottom: $check-loader-size/4;
  border: 4px solid rgba(0, 0, 0, 0.2);
  border-left-color: $check-color;
  animation: loader-spin 1.2s infinite linear;
  position: relative;
  display: inline-block;
  vertical-align: top;
  border-radius: 50%;
  width: $check-loader-size;
  height: $check-loader-size;
}

.load-complete {
  -webkit-animation: none;
  animation: none;
  border-color: $check-color;
  transition: border 500ms ease-out;
}

.checkmark {
  //display: none;

  &.draw:after {
    animation-duration: 800ms;
    animation-timing-function: ease;
    animation-name: checkmark;
    transform: scaleX(-1) rotate(135deg);
  }

  &:after {
    opacity: 1;
    height: $check-height;
    width: $check-width;
    transform-origin: left top;
    border-right: $check-thickness solid $check-color;
    border-top: $check-thickness solid $check-color;
    content: '';
    left: $check-left;
    top: $check-height;
    position: absolute;
  }
}

@keyframes loader-spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes checkmark {
  0% {
    height: 0;
    width: 0;
    opacity: 1;
  }
  20% {
    height: 0;
    width: $check-width;
    opacity: 1;
  }
  40% {
    height: $check-height;
    width: $check-width;
    opacity: 1;
  }
  100% {
    height: $check-height;
    width: $check-width;
    opacity: 1;
  }
}
</style>
