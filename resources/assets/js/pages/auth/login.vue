<template>
  <Row type="flex" justify="center" align="middle">
    <Col>
      <Card style="width:350px;">
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
          <FormItem prop="password" :show-message="form.errors.has('password')" :error="form.errors.get('password')">
            <Input 
              v-model="form.password"
              type="password" 
              name="password"  
              size="large" 
              :placeholder="$t('password')"
            >
              <Icon type="ios-locked-outline" slot="prepend"></Icon>
            </Input>
          </FormItem>
          <Row>
            <Col span="12">
              <FormItem prop="remember">
                <Checkbox v-model="remember" name="remember">{{ $t('remember_me') }}</Checkbox>
              </FormItem>
            </Col>
            <Col span="12">
              <router-link :to="{ name: 'password.request' }" class="small ml-auto my-auto">
                {{ $t('forgot_password') }}
              </router-link>
            </Col>
          </Row>

          <FormItem>
            <Button type="primary" @click="login" :loading="form.busy" long>
              {{ $t('login') }}
            </Button>
          </FormItem>

          <!-- GitHub Login Button -->
          <login-with-github/>

        </form>
      </card>
    </Col>
  </Row>
</template>

<script>
import Form from 'vform'

export default {
  metaInfo () {
    return { title: this.$t('login') }
  },

  data: () => ({
    form: new Form({
      email: '',
      password: ''
    }),
    remember: false
  }),

  methods: {
    async login () {
      try {

        // Submit the form.
        const { data } = await this.form.post('/api/login')

        // Save the token.
        this.$store.dispatch('auth/saveToken', {
          token: data.token,
          remember: this.remember
        })

        // Fetch the user.
        await this.$store.dispatch('auth/fetchUser')

        // Redirect home.
        this.$router.push({ name: 'home' })
      } catch (e) {
        console.log(e.response) // undefined
      }

      if(this.form.errors.any()){
        this.$Message.error('Fail!');
      }else{
        this.$Message.success('Success!');
      }

    }
  }
}
</script>
