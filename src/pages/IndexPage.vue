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
        color="teal"
        v-model="fidelidade"
        label="Possuo cartão fidelidade e desejo utilizar os descontos disponíveis."
      />
    </div>
    <div class="row q-mt-xl">
      <q-btn color="secondary" label="Calcular" @click="somaProduto()" />
    </div>
    <div class="q-mt-xl" v-if="verResultado">
      <h5>Produto:{{ nome }}</h5>
      <p><b>Quantidade:</b> {{ quantidade }}</p>
      <p><b>Valor unitário:</b> {{ preco }}</p>
      <p><b>Valor total:</b> {{ valorTotal }}</p>
      <p><b>Valor desconto:</b> {{ valorDesconto }}</p>
      <p><b>Total a pagar: </b>{{ valorPagar }}</p>
      <p>
        <i>{{ promocao }}</i>
      </p>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'IndexPage',

  // se tem promoção
  // +4 un tem 10% desconto total AQUI
  // valor unitario maior 50 tem 5% desconto
  // se possui fidelidade desconto de 5% no preço total (desconsidera outros descontos) OK
  // produto, quantidade, preço uni, preço total, valor de desconto, valor a ser pago

  setup() {
    let nome = ref('');
    let quantidade = ref('');
    let preco = ref('');
    let fidelidade = ref('');
    let valorTotal = ref('');
    let valorDesconto = ref('');
    let valorPagar = ref('');
    let verResultado = ref(false);
    let promocao = ref('');

    const somaProduto = () => {
      valorTotal.value = `${
        parseFloat(quantidade.value) * parseFloat(preco.value)
      }`;

      validaDescontos();
    };

    const validaDescontos = () => {
      verResultado.value = true;
      if (fidelidade.value == true) {
        let porcentagem = valorTotal.value * (5 / 100);
        valorPagar.value = valorTotal.value - porcentagem;
        valorDesconto.value = valorTotal.value - valorPagar.value;
        console.log(
          'fidelidade: ',
          valorTotal.value,
          valorPagar.value,
          valorDesconto.value
        );
        promocao.value = '* Produto com desconto fidelidade aplicado.';
      } else {
        if (quantidade.value >= 4) {
          let porcentagem = valorTotal.value * (10 / 100);
          valorPagar.value = valorTotal.value - porcentagem;
          valorDesconto.value = valorTotal.value - valorPagar.value;
          console.log(
            'qtd maior que 4: ',
            valorTotal.value,
            valorPagar.value,
            valorDesconto.value
          );
          promocao.value =
            '* Produto com promoção de 10% na compra de 4 unidades ou mais.';
        } else {
          valorPagar.value = valorTotal.value;
          valorDesconto.value = 0;
        }

        if (preco.value >= 50) {
          let porcentagem = valorTotal.value * (5 / 100);
          valorPagar.value = valorTotal.value - porcentagem;
          valorDesconto.value = valorTotal.value - valorPagar.value;
          console.log(
            'preco uni maior que 50: ',
            valorTotal.value,
            valorPagar.value,
            valorDesconto.value
          );
          promocao.value =
            '* Produto com 5% desconto na compra de produtos com preço acima de 50 reais.';
        } else {
          valorPagar.value = valorTotal.value;
          valorDesconto.value = 0;
        }
      }
    };

    return {
      nome,
      quantidade,
      preco,
      fidelidade,
      valorTotal,
      valorDesconto,
      valorPagar,
      verResultado,
      promocao,
      somaProduto,
      validaDescontos,
    };
  },
});
</script>
