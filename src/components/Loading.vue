<template>
   

<div class="hehe">
    <svg width="120" height="120">
            <circle cx="60" cy="60" r="20"></circle>
        </svg>
</div>

</template>

<script setup lang="ts">

</script>

<style scoped>
.hehe{
    background-color: rgba(0, 0, 0, 0.5);
    margin-left: -42px;
/*     margin-right: -41px;
    margin-top: -34px; */
    height: 100vh;
    width: 101vw;
    display: flex;
    justify-content: center;
    align-items: center;
}
@keyframes bouncedelay {
  0%, 80%, 100% {
    transform: scale(0.0);
  }
  40% {
    transform: scale(1.0);
  }
}

#css-animation-container {
  position: relative;
  top: 50%;
  width: 100%;
  height: 300px;
  display: inline-block;
}

#css-animation-container .div-center {
  width: 75px;
  height: 75px;
  top: 50%;
  left: 50%;
  position: absolute;
  transform: translate(-50%, -50%);
}

#css-animation-container [class^=container] {
  width: 100%;
  height: 100%;
  position: absolute;
}

#css-animation-container .container2 {
  transform: rotate(45deg);
}

#css-animation-container [class^=circle] {
  width: 16px;
  height: 16px;
  position: absolute;
  border-radius: 100%;
  background-color: blue;
  animation: bouncedelay 1.2s infinite ease-in-out;
}

#css-animation-container .circle1 {
  top: 0;
  left: 0;
}

#css-animation-container .circle2 {
  top: 0;
  right: 0;
}

#css-animation-container .circle3 {
  bottom: 0;
  right: 0;
}

#css-animation-container .circle4 {
  bottom: 0;
  left: 0;
}

#css-animation-container .container1 .circle1 {
  animation-delay: -1.05s;
}
#css-animation-container .container2 .circle1 {
  animation-delay: -0.9s;
}
#css-animation-container .container1 .circle2 {
  animation-delay: -0.75s;
}
#css-animation-container .container2 .circle2 {
  animation-delay: -0.6s;
}
#css-animation-container .container1 .circle3 {
  animation-delay: -0.45s;
}
#css-animation-container .container2 .circle3 {
  animation-delay: -0.3s;
}
#css-animation-container .container1 .circle4 {
  animation-delay: -0.15s;
}

@keyframes change {
            from {
                stroke-dasharray: 10 114.8;
            }

            to {
                stroke-dasharray: 104.8 20;
            }
        }

        @keyframes cc {
            from {
                stroke-dashoffset: 124.8;
            }

            66%{
                stroke-dashoffset: 62.4;
            }

            to {
                stroke-dashoffset: 0;
            }
        }

        circle {
            fill: none;
            stroke: yellowgreen;
            stroke-width: 5;
            stroke-dasharray: 104.8 20;
            animation: 0.8s cc,1.3s alternate change;
            animation-iteration-count: infinite;
            animation-timing-function: linear;
        }
</style>