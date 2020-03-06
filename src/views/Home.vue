<template>
  <main class="display-cards">
    <div class="show-card">
      <Top title="E-WALLET" subtitle="ACTIVE CARD" />
      <Card v-bind:card="selectedCard" />
    </div>
    <button class="delete-card" v-on:click="deleteCard(selectedId)">DELETE CARD</button>
    <div class="show-stack">
      <CardStack v-bind:cards="cards" v-on:sendID="selectThisCard" />
      <router-link to="/AddCard">
        <button class="add-card">ADD NEW CARD</button>
      </router-link>
    </div>
  </main>
</template>

<script>
import Top from "@/components/Top";
import Card from "@/components/Card";
import CardStack from "@/components/CardStack";

/* const STORAGE_KEY = "card-storage"; */
export default {
  components: { Top, Card, CardStack },
  data() {
    return {
      selectedId: 1
    };
  },
  computed: {
    cards() {
      return this.$root.$data.cards;
    },
    selectedCard() {
      return this.$root.$data.cards.find(card => card.id == this.selectedId);
    }
  },

  methods: {
    selectThisCard(id) {
      this.selectedId = id;
    },
    deleteCard() {
      this.$root.$emit("deleteCard", this.selectedId);
      this.$root$data.cards[0];

      // find index of selected card
      /*let ind = this.$root.$data.cards.findIndex(
        card => card.id === this.selectedCard.id
      );

      // remove card from card array with index
      this.$root.$data.cards.splice(ind, 1);

      // Update localstorage
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.$root.$data.cards));

      this.selectedCard = this.$root.$data.cards[0].id; 
    } */
    }
  }
};
</script>

<style>
.display-cards {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.show-card {
  color: black;
  margin-bottom: 200px;
}

.card {
  display: grid;
  grid-auto-rows: 4rem;
}

.card-item {
  z-index: 1;
}

button {
  margin-top: 190px;
  padding: 20px;
  border: solid 2px black;
  border-radius: 10px;
  width: 100%;
}

.delete-card {
  margin-top: 10px;
  margin-bottom: 30px;
  width: 15%;
}
</style>
