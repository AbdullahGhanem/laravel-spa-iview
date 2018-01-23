<template>
  <Dropdown>
    <a href="javascript:void(0)">
        {{ locales[locale] }}
        <Icon type="arrow-down-b"></Icon>
    </a>
    <DropdownMenu slot="list">
      <a v-for="(value, key) in locales" class="dropdown-item" href="#"
        @click.prevent="setLocale(key)">
        <DropdownItem>{{ value }}</DropdownItem>
      </a>
    </DropdownMenu>
  </Dropdown>
</template>

<script>
import { mapGetters } from 'vuex'
import { loadMessages } from '~/plugins/i18n'

export default {
  computed: mapGetters({
    locale: 'lang/locale',
    locales: 'lang/locales'
  }),

  methods: {
    setLocale (locale) {
      if (this.$i18n.locale !== locale) {
        loadMessages(locale)

        this.$store.dispatch('lang/setLocale', { locale })
      }
    }
  }
}
</script>
