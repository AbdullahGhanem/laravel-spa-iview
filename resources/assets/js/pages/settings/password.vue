<template>
  <Form :model="form" label-position="left" :label-width="100">
    <!-- Password -->
    <FormItem 
      :label="$t('password')" prop="password" 
      :show-message="form.errors.has('password')" 
      :error="form.errors.get('password')"
    >
      <Input 
        v-model="form.password"
        type="password" 
        name="password"  
        size="large" 
        :placeholder="$t('password')" 
        :class="{ 'is-invalid': form.errors.has('password') }"
      >
      </Input>
    </FormItem>

    <!-- Password Confirmation -->
    <FormItem 
      :label="$t('confirm_password')" prop="password_confirmation" 
      :show-message="form.errors.has('password_confirmation')" 
      :error="form.errors.get('password_confirmation')"
    >
      <Input 
        v-model="form.password_confirmation"
        type="password" 
        name="password_confirmation"  
        size="large" 
        :placeholder="$t('confirm_password')" 
      >
      </Input>
    </FormItem>

    <FormItem>
      <Button type="primary" @click="update" :loading="form.busy" long>
        {{ $t('update') }}
      </Button>
    </FormItem>
  </form>
</template>

<script>
import Form from 'vform'

export default {
  scrollToTop: false,

  metaInfo () {
    return { title: this.$t('settings') }
  },

  data: () => ({
    form: new Form({
      password: '',
      password_confirmation: ''
    })
  }),

  methods: {
    async update () {
      await this.form.patch('/api/settings/password')

      this.form.reset()
    }
  }
}
</script>
