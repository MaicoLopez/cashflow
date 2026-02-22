<template>
  <Layout>
    <template #header>
      <Header></Header>
    </template>
    <template #resume>
      <Resume
        :label="'Ahorro total'"
        :amount="amount"
        :total-amount="totalAmount"
      >
        <template #graphic>
          <Graphic :amounts="amounts" @select="select" />
        </template>
        <template #action> <Action @create="create" /> </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" @remove="remove" />
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
        // {
        //   id: 1,
        //   title: "Movimiento",
        //   description: "Deposito de salario",
        //   amount: 100,
        //   time: new Date("01-06-2026"),
        // },
        // {
        //   id: 2,
        //   title: "Movimiento 1",
        //   description: "Deposito de honorarios",
        //   amount: 200,
        //   time: new Date("01-06-2026"),
        // },
        // {
        //   id: 3,
        //   title: "Movimiento 2",
        //   description: "Comida",
        //   amount: 200,
        //   time: new Date("01-06-2026"),
        // },
        // {
        //   id: 4,
        //   title: "Movimiento 3",
        //   description: "Colegiatura",
        //   amount: -400,
        //   time: new Date("01-02-2026"),
        // },
        // {
        //   id: 5,
        //   title: "Movimiento 4",
        //   description: "Reparación equipo",
        //   amount: -600,
        //   time: new Date("01-02-2026"),
        // },
        // {
        //   id: 6,
        //   title: "Movimiento 5",
        //   description: "Reposición de efectivo",
        //   amount: -300,
        //   time: new Date("01-02-2026"),
        // },
        // {
        //   id: 7,
        //   title: "Movimiento 6",
        //   description: "Pago de servicios",
        //   amount: 100,
        //   time: new Date("01-02-2026"),
        // },
        // {
        //   id: 8,
        //   title: "Movimiento 7",
        //   description: "Ingreso de dinero",
        //   amount: 300,
        //   time: new Date("01-02-2026"),
        // },
        // {
        //   id: 9,
        //   title: "Movimiento 8",
        //   description: "Retiro de efectivo",
        //   amount: 500,
        //   time: new Date("01-02-2026"),
        // },
      ],
    };
  },
  computed: {
    amounts() {
      const lastDays = this.movements
        .filter((m) => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 60);
          return m.time > oldDate;
        })
        .map((m) => m.amount);

      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i + 1);
        return lastMovements.reduce((suma, movement) => {
          return suma + movement;
        }, 0);
      });
    },
    totalAmount() {
      return this.movements.reduce((suma, movement) => {
        return suma + movement.amount;
      }, 0);
    },
  },
  mounted() {
    const movements = JSON.parse(localStorage.getItem("movements"));
    if (Array.isArray(movements)) {
      this.movements = movements.map((m) => {
        return {
          ...m,
          time: new Date(m.time),
        };
      });
    }
  },
  methods: {
    create(movement) {
      this.movements.push(movement);
      this.save();
    },
    remove(id) {
      const index = this.movements.findIndex((m) => m.id === id);
      this.movements.splice(index, 1);
      this.save();
    },
    save() {
      localStorage.setItem("movements", JSON.stringify(this.movements));
    },
    select(amount) {
      this.amount = amount;
    },
  },
};
</script>
