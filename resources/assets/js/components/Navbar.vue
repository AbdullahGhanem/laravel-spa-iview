<template>
  <Header :style="{position: 'fixed', width: '100%', zIndex: '9999999999'}">
    <Menu mode="horizontal" theme="dark" active-name="1">
      <div class="layout-logo"></div>
        <div class="layout-nav">
          <MenuItem name="1">
            <router-link :to="{ name: user ? 'home' : 'welcome' }" class="navbar-brand">
              {{ appName }}
            </router-link>
          </MenuItem>
          <MenuItem name="2">
            <Icon type="ios-keypad"></Icon>
            Item 2
          </MenuItem>

          <div v-if="user" class="user-dropdown-menu-con">
            <Row type="flex" justify="end" align="middle" class="user-dropdown-innercon">
              <MenuItem name="3">
                  <locale-dropdown/>
              </MenuItem>
              <Dropdown transfer trigger="click" >
                  <a href="javascript:void(0)">
                    <span class="main-user-name">{{ user.name }}</span>
                    <Icon type="arrow-down-b"></Icon>
                  </a>
                  <DropdownMenu slot="list">
                    <router-link :to="{ name: 'settings.profile' }" >
                      <DropdownItem name="ownSpace">
                        <Icon type="ios-gear-outline"></Icon>
                        {{ $t('settings') }}
                      </DropdownItem>
                    </router-link>
                    <a @click.prevent="logout" href="#">
                      <DropdownItem name="logout">
                        <Icon type="log-out"></Icon>
                        {{ $t('logout') }}
                      </DropdownItem>
                    </a>
                  </DropdownMenu>
              </Dropdown>
              <Avatar :src="user.photo_url" style="background: #619fe7;margin-left: 10px;"></Avatar>
            </Row>
          </div>

          <!-- Guest -->
          <template v-else>
             <Row type="flex" justify="end" align="middle" class="user-dropdown-innercon">
            <MenuItem name="5">
              <router-link :to="{ name: 'login' }" class="nav-link" active-class="active">
                <Button>
                  <Icon type="log-in"></Icon>
                  {{ $t('login') }}
                </Button>
              </router-link>
            </MenuItem>
            <MenuItem name="6">
              <router-link :to="{ name: 'register' }" class="nav-link" active-class="active">
                <Button>
                  <Icon type="ios-personadd"></Icon>
                  {{ $t('register') }}
                </Button>
              </router-link>
            </MenuItem>
          </Row>
        </template>
      </div>
    </Menu>
  </Header>
</template>

<script>
import { mapGetters } from 'vuex'
import LocaleDropdown from './LocaleDropdown'

export default {
  data: () => ({
    appName: window.config.appName
  }),

  computed: mapGetters({
    user: 'auth/user'
  }),

  components: {
    LocaleDropdown
  },

  methods: {
    async logout () {
      // Log out the user.
      await this.$store.dispatch('auth/logout')

      // Redirect to login.
      this.$router.push({ name: 'login' })
    }
  }
}
</script>

