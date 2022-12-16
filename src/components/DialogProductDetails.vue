<template>
  <q-dialog
    :full-width="$q.plataform.is.mobile"
    :model-value="show"
    @before-hide="handleClose"
  >
    <q-card>
      <q-card-section>
        <div class="text-h6">
            Detalhes
        </div>
      </q-card-section>

      <q-card-section v-if="product.img_url">
        <q-img :src="product.img_url" :ratio="4/3" style="min-width: 300px" />
      </q-card-section>

      <q-card-section>
        <div class="text-h6">
            {{ product.name }}
        </div>
        <div class="text-subtitle2">
            {{ formatCurrency(product.price) }}
        </div>
        <div class="text-body2" v-html="product.description" ></div>
      </q-card-section>

      <q-card-actions>
        <q-btn label="Cancel" color="primary" v-close-popup />
        <q-btn
          label="Fazer pedido"
          icon="mdi-whatsapp"
          color="green-7"
          @click="handleSendWpp"
        />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
import { defineComponent } from 'vue'
import { formatCurrency } from 'src/utils/format'

export default defineComponent({
  name: 'DialogProductDetails',
  props: {
    show: {
      type: Boolean,
      required: true
    },
    product: {
      type: Object
    }
  },
  setup (props, { emit }) {
    const handleClose = () => {
      emit('hideDialog')
    }

    const handleSendWpp = () => {
      alert('enviado para o zap')
    }

    return {
      formatCurrency,
      handleClose,
      handleSendWpp
    }
  }
})
</script>
