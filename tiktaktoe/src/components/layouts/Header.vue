<template>
  <div class="header">
    <div class="container">
      <div class="row">
        <div class="col-xs-12 col-sm-12 col-md-6">
          <div class="logo-container">
            <img src="@/assets/images/logo.svg" alt="logo" class="logo" />
          </div>
        </div>
        <div class="col-xs-12 col-sm-12 col-md-6">
          <div class="title-container">
            <span class="position">Frontend Developer</span>
            <span class="document-title">Challenge</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "header",
};
</script>

<style lang="scss">
.header {
  background: #d8d8d8;
  padding-top: 30px;
  padding-bottom: 30px;
}
.title-container {
  text-align: right;
  @media (max-width: 768px) {
    display: none;
  }
}
.logo-container {
  text-align: left;
  @media (max-width: 768px) {
    text-align: center;
  }
}
.logo {
  width: 250px;
  @media (max-width: 768px) {
    width: 180px;
  }
}
.position,
.document-title {
  color: #2c2e30;
  display: block;
}
</style>
