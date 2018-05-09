<template>
  <div>
    <section>
      <div class="container">
        <div class="row">
          <div class="col-md-12 text-center jumbotron">
            <p>
              <span class="main-title">
                Target <br class="d-lg-none"> exclusive offer.
              </span>
              <span class="main-title-detail">
                $49 membership (reg. $99) + $15  credit <br class="d-none d-lg-block"> with qualifying purchase.*
              </span>
            </p>
            <!-- For Desktop -->
            <div class="form d-none d-lg-block text-left">
              <p>
                <input type="text" v-model="zipcode" v-on:keypress="checkIfNum()" v-bind:class="{ 'form-error': showError }" ref="searchZip" placeholder="Enter ZIP Code"><button @click="getData()" class="cta-main">Get Started</button>
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
                <input type="text" v-model="zipcode" v-on:keypress="checkIfNum()" v-bind:class="{ 'form-error-mobile': showError }" ref="searchZip" placeholder="Enter ZIP Code"><button @click="getData()" class="cta-main">Get Started</button>
              </p>
              <transition name="fade" appear>
                <p v-if="showError" class="show-error">
                  This Zipcode is invalid! Please try again.
                </p>
              </transition>
            </div>
            <p>
              <span class="main-fine-print">
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
  </div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'

export default {
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
    this.preloadImgs();
  },
  mounted: function () {
    // Set form focus
    this.$nextTick(() => this.$refs.searchZip.focus())
  },
  data: function () {
    return {
      images: [
        'pointer-blk.jpg', 
        'pointer-grey.jpg', 
        'pointer-orange.jpg', 
        'form-exclamation.jpg'
      ],
      results: {},
      showError: false,
      zipcode: '',
    }
  },
  methods: {
    getData: function () {
      let self = this
      
      this.$nextTick(() => this.$refs.searchZip.focus())

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
      // Accept only numbers, sourced from Deendayal Garg, via. Stackoverflow
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
    },
    preloadImgs: function () {
      // Preload form images
      const images = this.images

      images.forEach(function (imgName) {
        let image = new Image()
        image.src = imgName
      })
    }
  }
}
</script>

<style scoped>
.jumbotron {
  border-radius: 0px;
  color: #FFF;
  padding: 68px 15px;
  background: url('/target-bg.jpg')
}

.main-title {
  font-size: 48px;
  font-family: 'Scandia-Bold';
  line-height: 48px;
}

.main-title-detail {
  padding: 10px 20px 0px 20px;
  font-size: 20px;
  line-height: 24px;
}

.main-fine-print {
  font-size: 10px;
  max-width: 600px;
  padding: 0px 20px;
  margin: auto;
}

/* / Form Data /  */

input[type='text'] {
  font-family: 'Scandia-Bold';
  background: url('/pointer-grey.jpg') no-repeat scroll 16px 20px;
  border-radius: 2px 0px 0px 2px;
  padding: 4px 46px 0px 46px;
  background-color: #FFF;
  vertical-align: bottom;
  color: #414042;
  z-index: 10;
  height: 60px;
  width: 260px;
  border: none;
}

input[type='text']:focus, input[type='text']:active {
  background: url('/pointer-blk.jpg') no-repeat scroll 16px 20px;
  background-color: #FFF;
  z-index: 100;
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

.form {
  width: 400px;
  margin: auto;
}

.form-error {
  background: url('/pointer-orange.jpg') no-repeat scroll 16px 20px, url('/form-exclamation.jpg') no-repeat scroll 200px 0px !important;
  background-color: #FFF !important;
  color: #EF7C42 !important;
}

.form-error-mobile {
  background: url('/pointer-orange.jpg') no-repeat scroll 16px 20px, url('/form-exclamation.jpg') no-repeat scroll 100% 0px !important;
  background-color: #FFF !important;
  color: #EF7C42 !important;
}

.show-error {
  font-family: 'Scandia-Bold';
  text-transform: uppercase;
  color: #EF7C42;
  font-size: 11px;
}

/* / Results Data /  */

.results-header {
  font-family: 'Scandia-Bold';
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 1.5px;
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

/* / Media Queries /  */

@media only screen and (max-width: 600px) {
  .form {
    width: 100%;
  }

  input[type="text"] {
    width: 100%;
    display: block;
    border-radius: 2px;
    margin: auto;
  }

  .form > p > button {
    border-radius: 2px;
    width: 100%;
    margin: 10px 0px;
  }

  .main-title {
    font-size: 34px;
    line-height: 38px;
  }

  .main-title-detail {
    font-size: 16px;
  }
}
</style>
