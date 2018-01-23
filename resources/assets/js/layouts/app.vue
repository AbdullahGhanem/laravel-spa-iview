<template>
  <div class="layout">
    <Layout style="min-height:100vh">
      <navbar></navbar>
        <Content  :style="{margin: '88px 60px 0'}" >
          <child/>
        </Content>
      <Footer class="layout-footer-center">2017-2018 &copy; DeltaCodes</Footer>
    </Layout>
  </div>
</template>

<script>
import Navbar from '~/components/Navbar'

export default {
  name: 'app-layout',

  components: {
    Navbar
  }
}
</script>
<style scoped>
    .layout{
        border: 1px solid #d7dde4;
        background: #f5f7f9;
        position: relative;
        border-radius: 4px;
        overflow: hidden;
    }
    .layout-logo{
        width: 100px;
        height: 30px;
        background: #5b6270;
        border-radius: 3px;
        float: left;
        position: relative;
        top: 15px;
        left: 20px;
    }
    .layout-nav{
        width: 420px;
        margin: 0 auto;
        margin-right: 20px;
    }
    .layout-footer-center{
        text-align: center;
    }
</style>
