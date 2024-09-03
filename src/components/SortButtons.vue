<template>
  <div class="sort-buttons">
    <v-tooltip text="Сортировка по убыванию рейтинга">
      <template v-slot:activator="{ props }">
        <v-btn
          v-bind="props"
          icon="mdi-sort-descending"
          density="compact"
          variant="tonal"
          class="sort-btn"
          color="blue"
          @click="sort('desc')"
        />
      </template>
    </v-tooltip>

    <v-tooltip text="Сортировка по возрастанию рейтинга">
      <template v-slot:activator="{ props }">
        <v-btn
          v-bind="props"
          icon="mdi-sort-ascending"
          density="compact"
          variant="tonal"
          class="sort-btn"
          color="blue"
          @click="sort('asc')"
        />
      </template>
    </v-tooltip>

    <v-tooltip text="Сброс сортировки">
      <template v-slot:activator="{ props }">
        <v-btn
          v-bind="props"
          icon="mdi-sort"
          density="compact"
          variant="tonal"
          class="sort-btn"
          color="blue"
          @click="sort('reset')"
        />
      </template>
    </v-tooltip>
  </div>
</template>

<script setup>
const props = defineProps({
  cards: Array,
});

const emit = defineEmits(["update"]);

function sort(order) {
  let sortedCards = [...props.cards];

  if (order === "asc") {
    sortedCards.sort((a, b) => a.rating.rate - b.rating.rate);
  } else if (order === "desc") {
    sortedCards.sort((a, b) => b.rating.rate - a.rating.rate);
  } else if (order === "reset") {
    sortedCards.sort((a, b) => a.id - b.id);
  }

  emit("onSortedCards", sortedCards);
}
</script>

<style scoped>
.sort-buttons {
  display: flex;
  gap: 10px;
  justify-content: center;
  margin-bottom: 10px;
}
.sort-btn {
  position: relative;
}
</style>
