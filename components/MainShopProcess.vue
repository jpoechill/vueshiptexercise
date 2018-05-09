<template>
  <div>
    <section>
      <div class="container">
        <div class="row">
          <div class="col-md-12 text-center">
            <p>
              <span class="page-title">
                Everything you love about <br class="d-none d-lg-block"> Target at your fingertips.
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
                Our shoppers work <br class="d-lg-none"> their <br class="d-none d-lg-block"> magic.
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
  </div>
</template>

<style scoped>
.page-title {
  font-size: 36px;
  font-family: 'Scandia-Bold';
  margin: 50px 0px;
  line-height: 42px;
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

/* / Media Queries /  */

@media only screen and (max-width: 600px) {
  .no-padding > .row > .col-md-4 {
    padding: 0;
  }

  .page-title {
    font-size: 28px;
    line-height: 38px;
  }

  .thumbnail-title {
    font-size: 20px;
    line-height: 28px;
  }

  .thumbnail-detail {
    font-size: 14px;
  }
}

@media only screen and (min-width: 600px) {
  .no-padding {
    padding: 0px;
  }
}
</style>
