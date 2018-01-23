<template>
  <Row type="flex" justify="center" >
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

          <!-- Submit Button -->
          <FormItem>
            <Button type="primary" @click="send" :loading="form.busy" long>
              {{ $t('send_password_reset_link') }}
            </Button>
          </FormItem>
        </Form>
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
      email: ''
    })
  }),

  methods: {
    async send () {
      const { data } = await this.form.post('/api/password/email')

      this.status = data.status

      this.form.reset()
    }
  }
}
</script>
