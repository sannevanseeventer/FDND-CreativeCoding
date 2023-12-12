<script>
    import {gsap}  from "gsap/dist/gsap";    
    import { onMount } from 'svelte';

    onMount(() => {
    const parts = document.querySelectorAll('.menu-item');

const menuAnchor = document.querySelector('#hamburger');
const menuWrapper = document.querySelector('.menu-wrapper');

const tl = gsap.timeline();

menuAnchor.addEventListener('click', function() {
	if (!menuAnchor.classList.contains('is-active')) {
		this.classList.add('is-active');

		tl.to(menuWrapper, {
			y: 0,
			duration: 0.5
		});

		const tl2 = gsap.timeline();

		gsap.set(parts, { y: -150, opacity: 0 });

        const order = [0, 1, 2, 3, 4]; // Specify the order of items: Over, Expertise, Team, Kennisbank, Kansenkaart

order.forEach((index, i) => {
  const part = parts[index];
  tl2.to(
    part,
    {
      y: i === order.length - 1 ? 20 : 0,
      x: Math.random() > 0.5 ? -5 : 5,
      opacity: 1,
      rotate: Math.random() > 0.5 ? -2 : 2,
      ease: 'bounce',
      duration: 1,
      delay: i * 0.1 + (i === order.length - 1 ? 0.7 : 0.2),
    },
    i === order.length - 1 ? 0 : `-=${0.1}`
  );
});


		tl.add(tl2, '-=.2');
	} else {
		this.classList.remove('is-active');

		gsap.to(menuWrapper, {
			y: '-100%',
			duration: 0.5
		});

		gsap.to(parts, {
			opacity: 0,
			duration: 0.2
		});
	}
});

addEventListener('mousemove', e => {
	gsap.to('.inner-wrapper', {
		rotateY: gsap.utils.mapRange(0, innerWidth, -5, 5, e.pageX),
		rotateX: gsap.utils.mapRange(0, innerHeight, -5, 5, e.pageY),
		ease: 'power.out'
	});
});

});

</script>
<div class="container">
    <div id="hamburger">
      <span class="line"></span>
      <span class="line"></span>
      <span class="line"></span>
    </div>
  
    <div class="menu-wrapper">
      <div class="inner-wrapper">
        <div class="menu-item"> Over </div>
        <div class="menu-item"> Expertise </div>
        <div class="menu-item"> Team </div>
        <div class="menu-item"> Kennisbank</div>
        <div class="menu-item"> Kansenkaart</div>
      </div>
    </div>
  
  </div>

  <style>
@import url("https://fonts.googleapis.com/css?family=Montserrat&display=swap");

.container {
  width: 100%;
  height: 100%;
  padding: 16px;
}

#hamburger {
  cursor: pointer;
  width: 30px;
  margin: 16px;
  z-index: 10;
  position: relative;
}

#hamburger .line {
  width: 100%;
  height: 3px;
  background-color: #ffffff;
  display: block;
  margin: 8px auto;
  transition: all 0.15s ease-in-out;
}


.menu-wrapper {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  transform: translateY(-100%);
  background: transparent;
  display: grid;
  place-content: center;
  perspective: 700px;
}

.inner-wrapper {
  font-weight: 700;
  font-size: calc(8vw + 20px);
  letter-spacing: -0.6vw;
  white-space: nowrap;
  line-height: 0.97em;
  display: block;
  position: relative;
  text-transform: uppercase;
}
.inner-wrapper .menu-item {
  display: block;
  position: relative;
  margin-top: -0.25em;
  background: -webkit-linear-gradient(#ffffff 5%, rgba(255, 255, 255, 0.473) 85%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  cursor: pointer;
}
.inner-wrapper .menu-item:hover {
  background: -webkit-linear-gradient(#000000 5%, white 85%);
  -webkit-background-clip: text;
}
.inner-wrapper .menu-item:nth-child(1) {
  z-index: 0; /* Change the z-index to 0 for "Over" */
}
.inner-wrapper .menu-item:nth-child(2) {
  z-index: 1;
}
.inner-wrapper .menu-item:nth-child(3) {
  z-index: 2;
}
.inner-wrapper .menu-item:nth-child(4) {
  z-index: 3;
}
.inner-wrapper .menu-item:nth-child(5) {
  z-index: 4;
}
  </style>