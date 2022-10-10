<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <q-page padding>
      <div class="row justify-center">
          <div class="col-12 text-center">
              <p class="text-h6">
                  Form Category
              </p>
          </div>
          <q-form class="col-md7 col-xs-12 col-sm-12 q-gutter-y-md" @submit.prevent="handleSubmit">
            <q-input
              label="Name"
              v-model="form.name"
              :rules="[val => (val && val.length > 0) || 'Name is required']"
            />

            <q-btn
              label="Save"
              color="primary"
              class="full-width"
              rounded
              type="submit"
            />

            <q-btn
              label="Save"
              color="primary"
              class="full-width"
              rounded
              flat
              :to="{ name: 'category' }"
            />
          </q-form>
      </div>
  </q-page>
</template>

<script>
import { defineComponent, ref, onMounted, computed } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import useApi from 'src/composables/UseApi'
import useNotify from 'src/composables/UseNotify'

export default defineComponent({
  name: 'PageFormCategory',
  setup () {
    const table = 'category'
    const router = useRouter()
    const route = useRoute()
    const { post } = useApi()
    const { notifyError, notifySuccess } = useNotify()

    const isUpdate = computed(() => route.params.id)

    const form = ref({
      name: ''
    })

    onMounted(() => {
      if (isUpdate.value) {
        alert('É para atualizar')
      }
    })

    const handleSubmit = async () => {
      try {
        await post(table, form.value)
        notifySuccess('Saved Successfully')
        router.push({ name: 'category' })
      } catch (error) {
        notifyError(error.message)
      }
    }

    return {
      handleSubmit,
      form
    }
  }
})
</script>
