<template>
  <Layout>
    <template #header>
      <Header></Header>
    </template>
    <template #resume>
      <Resume :label="'Ahorro total'" :amount="amount" :total-amount="10000000">
        <template #graphic> <Graphic /> </template>
        <template #action> <Action /> </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" />
    </template>
  </Layout>
</template>
<script>
import Action from "./Action.vue";
import Graphic from "./Graphic.vue";
import Header from "./Header.vue";
import Layout from "./Layout.vue";
import Movements from "./Movements/index.vue";
import Resume from "./Resume/index.vue";
export default {
  components: {
    Layout,
    Header,
    Resume,
    Movements,
    Action,
    Graphic,
  },
  data() {
    return {
      amount: null,
      movements: [
        {
          id: 1,
          title: "Movimiento",
          description: "Deposito de salario",
          amount: 1000,
        },
        {
          id: 2,
          title: "Movimiento 1",
          description: "Deposito de honorarios",
          amount: 500,
        },
        {
          id: 3,
          title: "Movimiento 2",
          description: "Comida",
          amount: -100,
        },
        {
          id: 4,
          title: "Movimiento 3",
          description: "Colegiatura",
          amount: 1000,
        },
        {
          id: 5,
          title: "Movimiento 4",
          description: "Reparación equipo",
          amount: 1000,
        },
      ],
    };
  },
};
</script>
