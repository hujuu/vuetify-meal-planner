<script setup lang="ts">
import { ref } from "vue";
import CalendarCard from "@/components/CalendarCard.vue";

interface Today {
  id: number;
  title: string;
  readyInMinutes: number;
}

interface Card {
  date: Date;
  content: string;
  today: Today[];
}

const props = defineProps({
  date: {
    type: Date,
    required: true,
  },
  days: {
    type: Number,
    required: false,
    default: 7,
  },
  recipes: {
    type: Array,
    required: false,
    value: [],
  },
});

const generateCards = (startDate: Date, numberOfDays: number): Card[] => {
  const cards: Card[] = [];
  const currentDate = new Date(startDate);

  for (let i = 0; i < numberOfDays; i++) {
    const date = new Date(currentDate.getTime());
    const content = `Card ${i + 1}`;
    const recipesThisDay = (props.recipes || []).filter((recipe: any) => {
      const recipeDate = new Date(recipe.date).setHours(0, 0, 0, 0);
      return recipeDate === date.setHours(0, 0, 0, 0);
    }) as Today[];

    cards.push({ date, content, today: recipesThisDay });
    currentDate.setDate(currentDate.getDate() + 1);
  }

  return cards;
};
const cards = ref<Card[]>(generateCards(props.date, props.days));

</script>

<template>
  <v-table>
    <thead>
    <tr>
      <th class="text-left">Upcoming days</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="card in cards" :key="card.date.toString()">
      <td class="py-4">
        <calendar-card :card="card" />
      </td>
    </tr>
    </tbody>
  </v-table>
</template>

<style scoped>

</style>
