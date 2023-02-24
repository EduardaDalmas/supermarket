<template>
  <q-page class="q-ml-xl q-mt-md">
    <div class="row">
      <h3>Produtos</h3>
    </div>
    <div class="row">
      <div class="col-md-3 q-mr-md">
        <q-input outlined v-model="nome" label="Nome do produto" />
      </div>

      <div class="col-md-1 q-mr-md">
        <q-input
          type="number"
          outlined
          v-model="quantidade"
          label="Quantidade"
        />
      </div>
      <div class="col-md-2">
        <q-input
          type="number"
          outlined
          v-model="preco"
          label="Preço unitário do produto"
        />
      </div>
    </div>
    <div class="row q-mt-sm">
      <q-checkbox
        v-model="fidelidade"
        label="Possuo cartão fidelidade e desejo utilizar os descontos disponíveis."
      />
    </div>
  </q-page>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'IndexPage',

  // se tem promoção
  // +4 un tem 10% desconto total
  // valor unitario maior 50 tem 5% desconto
  // se possui fidelidade desconto de 5% no preço total (desconsidera outros descontos)
  // produto, quantidade, preço uni, preço total, valor de desconto, valor a ser pago

  setup() {
    let nome = ref(null);
    let quantidade = ref(null);
    let preco = ref(null);
    let fidelidade = ref(null);
    let valorTotal = ref(null);
    let valorDesconto = ref(null);
    let valorPagar = ref(null);

    // const validaDescontos = () => {};

    return {
      nome,
      quantidade,
      preco,
      fidelidade,
      valorTotal,
      valorDesconto,
      valorPagar,
      // validaDescontos,
    };
  },
});
</script>
