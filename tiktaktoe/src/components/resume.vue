<template>
  <div class="resume">
    <div class="container">
      <div class="row">
        <div class="col-xs-12 col-sm-12 col-md-6">
          <div class="avatar-container">
            <img
              src="@/assets/images/hesam.jpg"
              alt="hesamsameni"
              class="avatar"
            />
            <div class="info">
              <h2 class="name">Hesam Sameni</h2>
              <span class="meta"
                >Age: <span class="value">31 years old</span></span
              >
              <span class="meta"
                >Location: <span class="value">Lisbon</span></span
              >
              <span class="meta"
                >Occupation: <span class="value">Frontend Developer</span></span
              >
            </div>
          </div>
        </div>
        <div class="col-xs-12 col-sm-12 col-md-6">
          <div class="aboutme-container">
            <span class="title">About me:</span>
            <p class="paragraph">
              Web Designer / Developer Enjoy creating digital products, love to
              work in creative and young teams, always seeking to learn new
              things. I would love to work in teams with the goal of saving the
              environment.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "resume",
};
</script>

<style lang="scss">
.resume {
  padding-top: 60px;
  padding-bottom: 60px;
  .avatar {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    margin-right: 30px;
  }
  .avatar-container {
    display: flex;
    @media (max-width: 768px) {
      margin-bottom: 30px;
    }
    .info {
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      .meta {
        font-size: 16px;
        color: gray;
        .name {
          font-size: 25px;
        }
      }
    }
  }
  .aboutme-container {
    .title {
      display: block;
      font-size: 20px;
      font-weight: bold;
    }
    .paragraph {
      color: gray;
      font-size: 16px;
      text-align: left;
      line-height: 2em;
    }
  }
}
</style>
