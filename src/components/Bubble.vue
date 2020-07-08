<template>
  <div 
    class="bubble"
    :class="isUserMessage ? 'me' : 'you'"
  >
    {{msg}}
  </div>
</template>

<script>
export default {
  name: 'Bubble',
  props: {
    msg: String,
    isUserMessage: Boolean
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.bubble {
  font-size: 16px;
  position: relative;
  display: inline-block;
  clear: both;
  margin-bottom: 8px;
  padding: 13px 14px;
  vertical-align: top;
  border-radius: 5px;
  &:before {
    position: absolute;
    top: 19px;
    display: block;
    width: 8px;
    height: 6px;
    content: '\00a0';
    transform: rotate(29deg) skew(-35deg);
  }
  &.you {
    color: #fff;
    background-color: #00b0ff;
    align-self: flex-start;
    animation-name: slideFromLeft;
    &:before {
      left: -3px;
      background-color: #00b0ff;
    }
  }
  &.me {
    margin-left: auto;
    color: #1a1a1a;
    background-color: #eceff1;
    align-self: flex-end;
    animation-name: slideFromRight;
    &:before {
      right: -3px;
      background-color: #eceff1;
    }
  }
}

@keyframes slideFromLeft {
    0% {
        margin-left: -200px;
        opacity: 0;
    }
    100% {
        margin-left: 0;
        opacity: 1;
    }
}

@-webkit-keyframes slideFromLeft {
    0% {
        margin-left: -200px;
        opacity: 0;
    }
    100% {
        margin-left: 0;
        opacity: 1;
    }
}

@keyframes slideFromRight {
    0% {
        margin-right: -200px;
        opacity: 0;
    }
    100% {
        margin-right: 0;
        opacity: 1;
    }
}

@-webkit-keyframes slideFromRight {
    0% {
        margin-right: -200px;
        opacity: 0;
    }
    100% {
        margin-right: 0;
        opacity: 1;
    }
}
</style>
