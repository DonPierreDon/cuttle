<template>
  <v-dialog v-model="show">
    <!-- Activator -->
    <template #activator="{ props }">
      <slot name="button">
        <v-btn v-bind="props" color="primary" class="mb-2" variant="text" data-cy="ranked-info-button">
          <span v-if="showButtonText">How are ranks determined?</span>
          <v-icon class="ml-1" icon="mdi-information-outline" />
        </v-btn>
      </slot>
    </template>
    <!-- Dialog -->
    <v-card>
      <v-card-title class="d-flex justify-space-between">
        <h1>Ranked Scoring</h1>
        <v-btn icon @click="show = false" variant="text">
          <v-icon icon="mdi-close" size="large" />
        </v-btn>
      </v-card-title>
      <v-card-text>
        <p>
          Competitive Cuttle is divided into 4 seasons per year, one per suit: Clubs, Diamonds, Hearts, and
          Spades. At the end of each season, the top 8 players play a double elimination championship
          tournament and the
          <strong>champions are permanantly accoladed on the site.</strong>
        </p>
        <div class="d-flex justify-space-around flex-wrap mt-4">
          <award-card username="Champion player" :place="1" class="mb-4" />
          <award-card username="Second Place Player" :place="2" class="mb-4" />
          <award-card username="Third Place Player" :place="3" class="mb-4" />
        </div>
        <p>
          Each Season is divided into 13 weeks. For each week, we count the number of best 2/3 ranked matches
          each player wins against unique opponents (ignoring stalemates) and assign players points based on
          their weekly standing.
        </p>
        <v-list>
          <v-list-item>
            <v-chip variant="elevated" class="mr-2 mb-1" :color="theme.firstPlace"> 5 Points </v-chip>
            The player with the most wins gets 5 points for the week
          </v-list-item>
          <v-list-item>
            <v-chip variant="elevated" class="mr-2 mb-1" :color="theme.secondPlace"> 4 Points </v-chip>
            The player with the 2nd most wins gets 4 points for the week
          </v-list-item>
          <v-list-item>
            <v-chip variant="elevated" class="mr-2 mb-1" :color="theme.thirdPlace"> 3 Points </v-chip>
            The player with the 3rd most wins gets 3 points for the week
          </v-list-item>
          <v-list-item>
            <v-chip variant="outlined" class="mr-2 mb-1" :color="theme.primary"> 2 Points </v-chip>
            Each other player who won at least one match gets 2 points for the week
          </v-list-item>
          <v-list-item>
            <v-chip variant="outlined" class="mr-2 mb-1" color="#000"> 1 Point </v-chip>
            Each other player who completed a match without winning gets 1 point for the week
          </v-list-item>
        </v-list>
        <p>
          You can view the statistics and rankings for each season on this page. At the end of each season,
          the top 8 players compete in a double elimination championship tournament. At the end of the year,
          the top 8 players from the Season Championships compete in the Cuttle World Championship! Do you
          have what it takes to become
          <strong> Lord of the Deep? </strong>
        </p>
        <!-- Actions -->
        <v-card-actions class="d-flex justify-end">
          <v-btn variant="outlined" color="primary" @click="show = false"> Got It! </v-btn>
        </v-card-actions>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
import AwardCard from '@/components/AwardCard.vue';

export default {
  name: 'StatsScoringDialog',
  components: {
    AwardCard,
  },
  props: {
    showButtonText: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      show: false,
    };
  },
  computed: {
    theme() {
      return this.$vuetify.theme.themes.cuttleTheme.colors;
    },
  },
};
</script>
