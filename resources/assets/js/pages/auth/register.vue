<template>
  <Row type="flex" justify="center" >
    <Col>
      <Card style="width:350px;">
        <Form :model="form">
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
              name="confirm_password"  
              size="large" 
              :placeholder="$t('password_confirmation')" 
            >
            </Input>
          </FormItem>

          <FormItem>
            <Button type="primary" @click="register" :loading="form.busy" long>
              {{ $t('register') }}
            </Button>
          </FormItem>

              <!-- GitHub Register Button -->
              <login-with-github/>
            </div>
          </div>
        </form>
      </card>
    </Col>
  </Row>
</template>

<script>
import Form from 'vform'

export default {
  metaInfo () {
    return { title: this.$t('register') }
  },

  data: () => ({
    form: new Form({
      name: '',
      email: '',
      password: '',
      password_confirmation: ''
    })
  }),

  methods: {
    async register () {
      // Register the user.
      const { data } = await this.form.post('/api/register')

      // Log in the user.
      const { data: { token }} = await this.form.post('/api/login')

      // Save the token.
      this.$store.dispatch('auth/saveToken', { token })

      // Update the user.
      await this.$store.dispatch('auth/updateUser', { user: data })

      // Redirect home.
      this.$router.push({ name: 'home' })
    }
  }
}
</script>
