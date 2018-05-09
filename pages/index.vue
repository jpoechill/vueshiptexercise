<template>
  <div>
    <Header/>
      <MainExclusiveOffer/>
      <MainShopProcess/>
    <Footer/>
  </div>
</template>

<script>
import Header from '~/components/_Header.vue'
import MainExclusiveOffer from '~/components/MainExclusiveOffer.vue'
import MainShopProcess from '~/components/MainShopProcess.vue'
import Footer from '~/components/_Footer.vue'

export default {
  components: {
    Header,
    MainExclusiveOffer,
    MainShopProcess,
    Footer
  }
}
</script>

<style>
  /* / Globals /  */

  html, body {
    font-family: 'Scandia-Regular';
    color: #414042;
  }

  p span {
    display: block;
  }

  button {
    text-shadow: 0px 4px 20px rgba(0, 0, 0, .4 );
    background-color: #71B045;
    text-transform: uppercase;
    font-family: 'Scandia-Bold';
    letter-spacing: 1.5px;
    padding: 15px 23px;
    transition: .2s ease;
    border-radius: 2px;
    font-size: 11px;
    color: #FFF;
    border: none;
  }

  button:hover {
    background-color: #669933;
    text-shadow: none;
  }

  .cta-sml {
    margin: 30px 0px 20px 0px;
  }

  .cta-main {
    height: 60px;
    border-radius: 0px 2px 2px 0px;
  }

  .cta-lrg {
    box-shadow: 0px 2px 10px 0px rgba(0, 0, 0, .5);
    margin: 40px 0px 60px 0px;
    width: 320px;
    height: 60px;
  }
  
  /* / Media Queries /  */

  @media only screen and (max-width: 600px) {
    .cta-lrg {
      width: 100%;
    }
  }

  /* / Vue Transitions (Animations) /  */

  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }

</style>
