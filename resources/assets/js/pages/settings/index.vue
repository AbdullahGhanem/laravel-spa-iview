<template>
  <Layout>
    <Sider  hide-trigger :style="{background: '#fff'}">
      <Menu active-name="1" theme="light" width="auto">
        <div  v-for="tab in tabs">    
          <MenuItem name="7">
            <Icon :type="tab.icon"> </Icon>
            <router-link :to="{ name: tab.route }">
              {{ tab.name }}
            </router-link>
          </MenuItem>
        </div>
      </Menu>
    </Sider>
    <Content :style="{padding: '24px', minHeight: '280px', background: '#fff'}">
      <router-view></router-view>
    </Content>
  </Layout>
</template>

<script>
export default {
  loading: false,

  computed: {
    tabs () {
      return [
        {
          icon: 'person',
          name: this.$t('profile'),
          route: 'settings.profile'
        },
        {
          icon: 'ios-locked',
          name: this.$t('password'),
          route: 'settings.password'
        }
      ]
    }
  }
}
</script>

<style>
.settings-card .card-body {
  padding: 0;
}
</style>
