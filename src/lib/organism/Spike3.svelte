<script>
</script>
     

<div class="clouds">
    <div class="cloud"></div>
    <div class="cloud"></div>
    <div class="cloud"></div>
    <div class="cloud"></div>
    <div class="cloud"></div>
    <div class="cloud"></div>
    <div class="cloud"></div>
    <div class="cloud"></div>
    <div class="cloud"></div>
    <div class="cloud"></div>
  </div>
  <div class="balloon">
    <div class="logo"> <img class="logo" src="/logo_spatwater2.png" alt="logo spatwater"/></div>
    <div class="envelope"></div>
    <div class="basket"></div>
  </div>

<style>
:root {
  --color-cloud: #ffffff86;
  --color-balloon: rgb(113, 176, 200);
  --color-balloon-2: #5d8da5;
  --color-strings: #d9d9d9;
  --color-basket: #ceb89f;
  --size-cloud: 8rem;
  --size-balloon: 14rem;
  --animation-speed: 5s;
}

.clouds {
  position: absolute;
  top: 0%;
  left: 50%;
  transform: translate(-50%, -60%);
  width: var(--size-cloud);
  -webkit-animation: cloudsSlideDown var(--animation-speed) linear infinite;
          animation: cloudsSlideDown var(--animation-speed) linear infinite;
}
.cloud {
  position: relative;
  display: block;
  width: var(--size-cloud);
  height: var(--size-cloud);
  margin: 1rem;
  background-color: var(--color-cloud);
  border-radius: 50%;
}
.cloud:nth-child(5n + 1) {
  transform: translateX(-120%);
  margin-top: calc(var(--size-cloud) * 2);
}
.cloud:nth-child(5n + 2) {
  transform: translate(-220%, 20%) scale(0.5);
}
.cloud:nth-child(5n + 3) {
  transform: translate(150%, 20%) scale(0.8);
}
.cloud:nth-child(5n + 4) {
  transform: translate(-250%, 40%) scale(1.2);
}
.cloud:nth-child(5n + 5) {
  transform: translate(90%, 120%) scale(0.6);
}
.cloud::before,
.cloud::after {
  position: absolute;
  bottom: 0;
  display: block;
  width: var(--size-cloud);
  height: calc(var(--size-cloud) * 0.6);
  background-color: var(--color-cloud);
  border-radius: var(--size-cloud);
  transform: translateX(-30%);
  content: '';
}
.cloud::after {
  height: calc(var(--size-cloud) * 0.5);
  transform: translateX(23%);
}

.logo{
    background-image: url(./logo_spatwater2.png);
    background-size: contain;
    background-repeat: no-repeat;
    z-index: 2;
    position: absolute;
}

.balloon {
  display: block;
  z-index: 3;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  -webkit-animation: balloonBounce var(--animation-speed) infinite;
          animation: balloonBounce var(--animation-speed) infinite;
  perspective-origin: 50% 100%;
  perspective: calc(var(--size-balloon) * 0.5);
}
.balloon > .envelope {
  position: relative;
  display: block;
  width: var(--size-balloon);
  height: var(--size-balloon);
  background-color: var(--color-balloon);
  border-radius: var(--size-balloon);
  perspective-origin: 50% 100%;
  perspective: calc(var(--size-balloon) * 0.5);
}
 .balloon > .envelope::before,
.balloon > .envelope::after {
  position: absolute;
  display: block;
  content: '';
}
.balloon > .envelope::after {
  top: 2%;
  left: 50%;
  width: 38%;
  height: 80%;
  background-color: var(--color-balloon-2);
  transform: translateX(-50%);
  border-radius: 50%;
  z-index: 1;
}
.balloon > .envelope::before {
  top: 15%;
  width: calc(var(--size-balloon));
  height: calc(var(--size-balloon) * 2.2);
  border-radius: calc(var(--size-balloon) / 11);
  background: var(--color-balloon);
  transform: translateZ(calc(var(--size-balloon) * -0.94)) rotateX(-58deg);
} 


.balloon > .basket {
  position: absolute;
  top: 114%;
  left: 50%;
  display: block;
  width: calc(var(--size-balloon) / 5);
  height: calc(var(--size-balloon) / 10);
  background: linear-gradient(to right, var(--color-strings) 0%, var(--color-strings) 10%, var(--color-bg) 10%, var(--color-bg) 30%, var(--color-strings) 30%, var(--color-strings) 40%, var(--color-bg) 40%, var(--color-bg) 60%, var(--color-strings) 60%, var(--color-strings) 70%, var(--color-bg) 70%, var(--color-bg) 90%, var(--color-strings) 90%, var(--color-strings) 100%);
  border-radius: calc(var(--size-balloon) / 40);
  border-bottom: calc(var(--size-balloon) / 5.5) solid var(--color-basket);
  transform: translateX(-50%) rotateX(-20deg);
}
@-webkit-keyframes cloudsSlideDown {
  0% {
    transform: translate(-50%, -60%);
  }
  100% {
    transform: translate(-50%, -10%);
  }
}
@keyframes cloudsSlideDown {
  0% {
    transform: translate(-50%, -60%);
  }
  100% {
    transform: translate(-50%, -10%);
  }
}
@-webkit-keyframes balloonBounce {
  0% {
    transform: translate(-50%, -50%);
  }
  50% {
    transform: translate(-50%, -60%);
  }
  100% {
    transform: translate(-50%, -50%);
  }
}
@keyframes balloonBounce {
  0% {
    transform: translate(-50%, -50%);
  }
  50% {
    transform: translate(-50%, -60%);
  }
  100% {
    transform: translate(-50%, -50%);
  }
}

 </style>