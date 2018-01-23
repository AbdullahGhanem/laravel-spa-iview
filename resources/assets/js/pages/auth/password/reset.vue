<template>
  <Row type="flex" justify="center" align="center" >
    <Col>
      <Card style="width:350px;">
        <p slot="title" >
            <Icon type="ios-film-outline"></Icon>
            {{ $t('reset_password') }}
        </p>
        <Form :model="form">
          <!-- Email -->
          <FormItem prop="email" :show-message="form.errors.has('email')" :error="form.errors.get('email')">
            <Input 
              v-model="form.email" 
              type="email" 
              name="email" 
              size="large"
              :placeholder="$t('email')" 
            >
              <Icon type="at" slot="prepend"></Icon>
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
            :label="$t('password_confirmation')" prop="password_confirmation" 
            :show-message="form.errors.has('password_confirmation')" 
            :error="form.errors.get('password_confirmation')"
          >
            <Input 
              v-model="form.password_confirmation"
              type="password" 
              name="password_confirmation"  
              size="large" 
              :placeholder="$t('password_confirmation')" 
            >
            </Input>
          </FormItem>

          <FormItem>
            <Button type="primary" @click="reset" :loading="form.busy" long>
              {{ $t('login') }}
            </Button>
          </FormItem>

        </form>
      </card>
    </Col>
  </Row>
</template>

<script>
import Form from 'vform'

export default {
  metaInfo () {
    return { title: this.$t('reset_password') }
  },

  data: () => ({
    status: '',
    form: new Form({
      token: '',
      email: '',
      password: '',
      password_confirmation: ''
    })
  }),

  created () {
    this.form.email = this.$route.query.email
    this.form.token = this.$route.params.token
  },

  methods: {
    async reset () {
      const { data } = await this.form.post('/api/password/reset')

      this.status = data.status

      this.form.reset()
    }
  }
}
</script>
