<template>
  <div id="app">
    <div class="container">
      <div class="section"></div>
      <div class="section"></div>
      <div class="section"></div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  data() {
    return {
      windowScroll: window.scrollY,
      currentSection: 1,
      positionY: 1,
      scrollDown: 0,
    };
  },
  mounted() {
    this.scrollFullPage();
  },
  methods: {
    // scrollFullPage() {
    //   const container = document.querySelector('#app');
    //   const sections = container.querySelectorAll('.section');
    //   const sizeHeigthScreen = window.innerHeight;
    //   console.log(sizeHeigthScreen);
    //   window.onscroll = () => {
    //     const positionY = window.scrollY;
    //     const resultDivision = positionY / (100 * 2);
    //     console.log(positionY);
    //     if (Number.isInteger(resultDivision)) {
    //       this.currentSection++;
    //       sections[this.currentSection].scrollIntoView(
    //         { behavior: 'smooth' },
    //         true
    //       );
    //     }
    //   };
    // },
    // scrollFullPage() {
    //   const container = document.querySelector('#app');
    //   const sections = container.querySelectorAll('.section');
    //   window.onscroll = () => {
    //     if (window.scrollY % 100 === 0) {
    //       sections[this.currentSection].style.transform = 'translateY(200%)';
    //       sections[this.currentSection].style.zIndex = '1';
    //       this.currentSection++;
    //       sections[this.currentSection].style.transform = 'translateY(0%)';
    //       sections[this.currentSection].style.zIndex = '2';
    //     }
    //     console.log(sections);
    //   };
    // },
    scrollFullPage() {
      const container = document.querySelector('.container');
      const sections = container.querySelectorAll('.section');
      window.onscroll = () => {
        if (this.currentSection === 3)
          container.innerHTML += '<div style="height: 100px;"><div>';

        if (window.scrollY % 100 === 0 && window.scrollY !== 0) {
          this.scrollDown = 100 * this.currentSection;
          container.style.transform = `translateY(-${this.scrollDown}vh)`;
          this.currentSection++;
          window.scrollTo(0, 0);
          window.addEventListener('scroll', this.bloquearScroll, {
            passive: false,
          });
          setTimeout(function () {
            window.removeEventListener('scroll', this.bloquearScroll, {
              passive: false,
            });
          }, 5000);
        } else if (this.scrollDown === 200 && window.scrollY !== 0) {
          console.log('hi!');
          container.style.transform = `translateY(0vh)`;
          this.currentSection = 1;
          this.scrollDown = 0;
          window.scrollTo(0, 0);
        }
      };
    },
    bloquearScroll(event) {
      event.preventDefault();
    },
  },
};
</script>

<style>
.container {
  width: 100%;
  height: 3vh;
  position: absolute;
  left: 0;
  top: 0;
}
body {
  all: initial;
}
.section {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100vh;
  background: #333;
  transition: 1s ease-in-out;
}

.section:nth-child(2) {
  background: #334;
  transition: 1s ease-in-out;
}

.section:nth-child(3) {
  background: #343;
  transition: 1s ease-in-out;
}
</style>
