<template>
  <div>
    <header>
      <div class="info-bar text-center">
        Get $50 Off + $15 Credit*
      </div>
      <div class="container">
        <div class="header-container row">
          <div class="col text-left">
            <img src="/shipt-logo.jpg" alt="Shipt-logo">
          </div>
          <div class="col text-right">
            <button>
              SIGN UP
            </button>
          </div>
        </div>
      </div>
    </header>

    <section>
      <div class="container">
        <div class="row">
          <div class="col-md-12 text-center jumbotron">
            <p>
              <span class="main-title">
                Target exclusive offer.
              </span>
              <span class="main-title-detail">
                $49 membership (reg. $99) + $15 credit <br> with qualifying purchase.*
              </span>
            </p>
            <!-- For Desktop -->
            <div class="form d-none d-lg-block text-left">
              <p>
                <input type="text" v-model="zipcode" v-on:keypress="checkIfNum(evt)" v-bind:class="{ 'form-error': showError }" placeholder="Enter ZIP Code"><button @click="getData()" class="cta-main">Get Started</button>
              </p>
              <transition name="fade" appear>
                <p v-if="showError" class="show-error">
                  This Zipcode is invalid! Please try again.
                </p>
              </transition>
            </div>
            <!-- For Mobile -->
            <div class="form d-lg-none text-center">
              <p>
                <input type="text" v-model="zipcode" v-on:keypress="checkIfNum(evt)" placeholder="Enter ZIP Code"><button @click="getData()" class="cta-main">Get Started</button>
              </p>
              <transition name="fade" appear>
                <p v-if="showError" class="show-error">
                  This Zipcode is invalid! Please try again.
                </p>
              </transition>
            </div>
            <p>
              <span class="fine-print">
                *Membership offer valid for new members only. Target order of $100 or more must be placed to qualify for $15 credit, which expires 30 days after qualifying order is place and can be applied to any order from Shipt.
              </span>
            </p>
          </div>
        </div>
      </div>
    </section>

    <transition name="fade" appear>
      <section v-if="results.stores">
          <div class="container">
            <div class="row">
              <div class="col-md-12 results-header text-center">
                <p>
                  <span>
                    Delivering From:
                  </span>
                </p>
              </div>
              <div class="col-md-12 text-center">
                <div v-for="store in sortedArray" v-bind:key="store.name" class="result-container">
                  <p>
                    <span class="stores-name">
                      {{ store.name }}
                    </span>
                  </p>
                  <p>
                    <span class="stores-launch-date">
                      {{ convertUTC(store.launch_date) }}
                    </span>
                  </p>
                </div>
              </div>
            </div>
          </div>
          <div class="container">
            <div class="row">
              <div class="col-md-12 text-center">
                <button class="cta-sml">Get Started</button>
              </div>
            </div>
          </div>
      </section>
    </transition>

    <section>
      <div class="container">
        <div class="row">
          <div class="col-md-12 text-center">
            <p>
              <span class="page-title">
                Everything you love about <br> Target at your fingertips.
              </span>
            </p>
          </div>
        </div>
      </div>
      <div class="container no-padding">
        <div class="row">
          <div class="col-md-4 text-center">
            <img class="thumbnail-img" src="/thumbnails/step-01-thumbnail.jpg" alt="Woman making order on mobile phone">
            <p>
              <span class="thumbnail-title">
                Scroll through <br> the aisles.
              </span>
              <span class="thumbnail-detail">
                Create an order from your local store <br> in out app or on our website.
              </span>
            </p>
          </div>
          <div class="col-md-4 text-center">
            <img class="thumbnail-img" src="/thumbnails/step-02-thumbnail.jpg" alt="Shopper picking up groceries in store">
            <p>
              <span class="thumbnail-title">
                Our shoppers work their <br> magic.
              </span>
              <span class="thumbnail-detail">
                Connect with your shopper and get <br> live updates from the aisles.
              </span>
            </p>
          </div>
          <div class="col-md-4 text-center">
            <img class="thumbnail-img" src="/thumbnails/step-03-thumbnail.jpg" alt="Shopper delivering groceries to home">
            <p>
              <span class="thumbnail-title">
                We deliver <br> your groceries.
              </span>
              <span class="thumbnail-detail">
                Schedule a delivery, and your order <br> will arrive in as soon as 1 hour.
              </span>
            </p>
          </div>
        </div>
      </div>
      <div class="container">
        <div class="row">
          <div class="col-md-12 text-center">
            <button class="cta-lrg">Get Started</button>
          </div>
        </div>
      </div>
    </section>

    <footer>
      <div class="footer text-center">
        © 2018 Shipt, Inc. and its services are not necessarily affiliated or endorsed by the retailers on this site.
      </div>
    </footer>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import axios from 'axios'
import moment from 'moment'

export default {
  components: {
    Logo
  },
  computed: {
    sortedArray: function() {
      let newArr = this.results.stores.slice()
      return newArr.sort(function(a, b){
          if(a.name < b.name) return -1;
          if(a.name > b.name) return 1;
          return 0;
      })
    }
  },
  created: function () {
    const image = new Image();

    image.src = '/pointer-orange.jpg'
  },
  data: function () {
    return {
      results: {},
      showError: false,
      zipcode: '',
    }
  },
  methods: {
    getData: function () {
      let self = this

      axios
        .get('https://shipt-zip-code-test-api.herokuapp.com/api/zip_codes/' + this.zipcode)
        .then(function (response) {
          // Data success
          self.results = response.data
        })
        .catch(function (error) {
          // Error handling
          self.showError = true

          setTimeout(function(){ 
            self.showError = false 
            self.zipcode = ''
          }, 5000)
      });
    },
    checkIfNum: function (evt) {
      // Snippet below sourced from Deendayal Garg, Stackoverflow
      evt = (evt) ? evt : window.event;
      
      var charCode = (evt.which) ? evt.which : evt.keyCode;
      if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
        evt.preventDefault();;
      } else {
        return true;
      }
    },
    convertUTC: function (utcDate) {
      let today = new moment()
      let launchDate = moment.utc(utcDate)
      
      if (launchDate.isBefore(today)) {
        return 'Now Available'
      } else {
        return 'Coming ' + (Number(launchDate.format('m') + 1)) + '/' + launchDate.format('YY')
      }
    }
  }
}
</script>

<style>
html, body {
  font-family: 'Scandia-Regular';
  color: #414042;
}

p span {
  display: block;
}

::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
    color: #9F9F9F;
    opacity: 1; /* Firefox */
}

:-ms-input-placeholder { /* Internet Explorer 10-11 */
    color: #9F9F9F;
}

::-ms-input-placeholder { /* Microsoft Edge */
    color: #9F9F9F;
}

input[type='text'] {
  font-family: 'Scandia-Bold';
  background: url('/pointer-grey.jpg') no-repeat scroll 16px 20px;
  border-radius: 2px 0px 0px 2px;
  padding: 4px 46px 0px 46px;
  background-color: #FFF;
  vertical-align: bottom;
  /* transition: .2s ease; */
  color: #414042;
  z-index: 10;
  height: 60px;
  width: 260px;
  border: none;
}

input[type='text']:focus {
  background: url('/pointer-blk.jpg') no-repeat scroll 16px 20px;
  background-color: #FFF;
  z-index: 100;
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

.form {
  width: 400px;
  margin: auto;
}

.form-error {
  background: url('/pointer-orange.jpg') no-repeat scroll 16px 20px, url('/form-exclamation.jpg') no-repeat scroll 200px 0px !important;
  background-color: #FFF !important;
  color: #EF7C42 !important;
}

.show-error {
  font-family: 'Scandia-Bold';
  text-transform: uppercase;
  color: #EF7C42;
  font-size: 11px;
}

header {
  box-shadow: 0px 2px 10px 0px rgba(0, 0, 0, .1);
  background-color: #FFF;
}

.header-container {
  padding: 18px 0px;
}

.info-bar {
  background-color: #414042;
  font-family: 'Scandia-Bold';
  text-transform: uppercase;
  letter-spacing: 1.5px;
  font-size: 11px;
  transition: background-color .2s ease;
  padding: 4px 0px;
  color: #FFF;
  width: 100%;
}

.info-bar:hover {
  background-color: #71B045
}

.jumbotron {
  border-radius: 0px;
  color: #FFF;
  padding: 68px 15px;
  margin-top: 16px;
  background: url('/target-bg.jpg')
}

.main-title {
  font-size: 48px;
  font-family: 'Scandia-Bold';
  line-height: 48px;
}

.main-title-detail {
  padding-top: 10px;
  font-size: 20px;
  line-height: 24px;
}

.fine-print {
  font-size: 10px;
  max-width: 600px;
  padding: 0px 20px;
  margin: auto;
}

.page-title {
  font-size: 36px;
  font-family: 'Scandia-Bold';
  margin-top: 60px;
  line-height: 42px;
}

.results-header {
  font-family: 'Scandia-Bold';
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: .5px;
}

.result-container {
  display: inline-block;
  min-width: 240px;
  padding: 0px 50px;
  margin-bottom: 10px;
  text-align: center;
}

.stores-name {
  font-family: 'Scandia-Bold';
  font-size: 28px;
}

.stores-launch-date {
  font-family: 'Scandia-Bold';
  letter-spacing: 1.5px;
  color: #7B7B7B;
  font-size: 11px;
}

.thumbnail-img {
  box-shadow: 0px 15px 25px rgba(0, 0, 0, .05);
  margin: 30px 0px;
  width: 100%;
}

.thumbnail-title {
  font-size: 24px;
  font-family: 'Scandia-Bold';
  color: #414042;
}

.thumbnail-detail {
  font-size: 16px;
  margin: 14px 0px;
  color: #7B7B7B;
}

.cta-lrg {
  box-shadow: 0px 2px 2px 0px rgba(0, 0, 0, .5);
  margin: 40px 0px 60px 0px;
  width: 320px;
  height: 60px;
}

.cta-sml {
  margin: 30px 0px 0px 0px;
}

.cta-main {
  height: 60px;
  border-radius: 0px 2px 2px 0px;
}

.footer {
  background-color: #414042;
  color: rgba(247, 244, 234, .5);
  font-size: 11px;
  padding: 30px 0px;
}

/* /
  Vue Transitions (Animations)
/  */

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

/* /
  Media Queries
/  */

@media only screen and (max-width: 600px) {
  .no-padding > .row > .col-md-4 {
    padding: 0px;
  }

  .form {
    width: 100%;
  }

  input[type="text"] {
    width: 90%;
    display: block;
    border-radius: 2px;
    margin: auto;
  }

  .form > p > button {
    border-radius: 2px;
    width: 90%;
    margin: 10px 0px;
  }
}

@media only screen and (min-width: 600px) {
  .no-padding {
    padding: 0px;
  }
}
</style>
