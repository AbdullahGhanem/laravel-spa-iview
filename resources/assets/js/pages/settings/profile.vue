<template>
  <Form :model="form" label-position="left" :label-width="100">
    <!-- Name -->
    <FormItem :label="$t('name')" prop="name" :show-message="form.errors.has('name')" :error="form.errors.get('name')">
      <Input 
        v-model="form.name" 
        type="text" 
        name="name" 
        size="large"
        :placeholder="$t('name')" 
      >
      </Input>
    </FormItem>

    <!-- Email -->
    <FormItem :label="$t('email')" prop="email" :show-message="form.errors.has('email')" :error="form.errors.get('email')">
      <Input 
        v-model="form.email" 
        type="email" 
        name="email" 
        size="large"
        :placeholder="$t('email')" 
      >
      </Input>
    </FormItem>

    <!-- Submit Button -->
    <FormItem>
      <Button type="primary" @click="update" :loading="form.busy" long>
        {{ $t('update') }}
      </Button>
    </FormItem>
  </form>
</template>

<script>
import Form from 'vform'
import { mapGetters } from 'vuex'

export default {
  scrollToTop: false,

  metaInfo () {
    return { title: this.$t('settings') }
  },

  data: () => ({
    form: new Form({
      name: '',
      email: ''
    })
  }),

  computed: mapGetters({
    user: 'auth/user'
  }),

  created () {
    // Fill the form with user data.
    this.form.keys().forEach(key => {
      this.form[key] = this.user[key]
    })
  },

  methods: {
    async update () {
      const { data } = await this.form.patch('/api/settings/profile')

      this.$store.dispatch('auth/updateUser', { user: data })
    }
  }
}
</script>
