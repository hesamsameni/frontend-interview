<template>
  <div class="footer">
    <div class="container">
      <div class="row">
        <div class="col-xs-12 col-sm-12 col-md-4">
          <div class="section">
            <span class="title"> About Page </span>
            <span class="item">
              Play <span class="red">tic tac toe </span>any time!
            </span>
            <span class="item"
              >Created by
              <a href="https://www.linkedin.com/in/hesamsameni/"
                >Hesam Sameni</a
              ></span
            >
          </div>
        </div>
        <div class="col-xs-12 col-sm-12 col-md-4">
          <div class="section">
            <span class="title"> Contact Us </span>
            <span class="item"> (+351) 912076838 </span>
            <span class="item">Rua Sa da Bandira, 111, Porto</span>
          </div>
        </div>
        <div class="col-xs-12 col-sm-12 col-md-4">
          <div class="section">
            <span class="title"> Stay In Touch </span>
            <div class="social-wrapper">
              <a href="https://twitter.com/hesamsameni">
                <img
                  src="@/assets/images/twitter.svg"
                  alt="social"
                  class="social"
                />
              </a>
              <a href="https://www.instagram.com/hesamsameni/?hl=en">
                <img
                  src="@/assets/images/instagram.svg"
                  alt="social"
                  class="social"
                />
              </a>
              <a href="https://www.facebook.com/hesam.sameni/">
                <img
                  src="@/assets/images/facebook.svg"
                  alt="social"
                  class="social"
                />
              </a>
            </div>
            <div class="item">
              <input
                type="text"
                class="custom-input"
                placeholder="Subscribe to our games"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "footer",
};
</script>

<style lang="scss">
.footer {
  padding-top: 70px;
  padding-bottom: 70px;
  background: #ededed;
  .section {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    margin-bottom: 45px;
    .title {
      color: gray;
      font-size: 16px;
      font-weight: bold;
      margin-bottom: 15px;
    }
    .item {
      margin-bottom: 5px;
      font-size: 16px;
      color: gray;
      .custom-input {
        border: none;
        padding: 10px 5px;
        border-radius: 2px;
      }
      a {
        color: gray;
        text-decoration: none;
      }
      .red {
        color: #ff5c5b;
      }
    }
    .social-wrapper {
      display: flex;
      justify-content: flex-start;
      align-items: center;
      margin-bottom: 10px;
      .social {
        width: 30px;
        margin-right: 5px;
      }
    }
  }
}
</style>
