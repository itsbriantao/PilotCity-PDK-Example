<template>
  <v-container class="module-outcomes">
    <div class="module-outcomes__container">
      <div class="module-outcomes__items">
        <!-- <div class="module-outcomes__label text-body-1 font-weight-black">
          Minimum amount of minutes required before unlocking
        </div>
        <div class="module-outcomes__dropdown">
          <v-menu offset-y top>
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                block
                class="module-outcomes__select text-capitalize"
                outlined
                v-bind="attrs"
                v-on="on"
              >
                {{minReq}}
                <v-icon left class="ml-1">mdi-chevron-down</v-icon>
              </v-btn>
            </template>
            <v-list>
              <v-list-item
                v-for="(op, index) in minutesReq"
                :key="index"
                @click="minReq=op"
              >
                <v-list-item-title>{{ op }}</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>
        </div>
        <div class="module-outcomes__label  text-body-1 font-weight-black">
          Amount of minutes desired as a goal from organizer
        </div>
        <div class="module-outcomes__dropdown">
          <v-menu offset-y top>
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                block
                class="module-outcomes__select text-capitalize"
                outlined
                v-bind="attrs"
                v-on="on"
              >
                {{goal}}
                <v-icon left class="ml-1">mdi-chevron-down</v-icon>
              </v-btn>
            </template>
            <v-list>
              <v-list-item
                v-for="(op, index) in minutesNec"
                :key="index"
                @click="goal=op"
              >
                <v-list-item-title>{{ op }}</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>
        </div> -->
        <v-checkbox v-model="checkbox" class="module-outcomes__labels">
          <template v-slot:label>
            <div class="text-body-1 font-weight-black">
              Require students to acknowledge section completion
            </div>
          </template>
        </v-checkbox>
        <div class="module-outcomes__labels text-h6 font-weight-black">
          Employer
        </div>
        <v-text-field outlined hint="The name of your company or organization">
          <template v-slot:label>
            <span class="font-weight-black">Name</span>
          </template>
        </v-text-field>
        <v-text-field outlined>
          <template v-slot:label>
            <span class="font-weight-black">Website</span>
          </template>
        </v-text-field>
        <!-- <v-text-field outlined placeholder=" ">
          <template v-slot:label>
            <span class="font-weight-black">Email</span>
          </template>
        </v-text-field> -->
        <div class="module-outcomes__labels text-h6 font-weight-black">
          Social
        </div>
        <!-- <v-container class="pa-0">
          <v-row>
            <v-col>
              <v-text-field outlined placeholder=" " hide-details>
                <template v-slot:label>
                  <span class="font-weight-black">LinkedIn</span>
                </template>
              </v-text-field>
            </v-col>
            <v-col>
              <v-text-field outlined placeholder=" " hide-details>
                <template v-slot:label>
                  <span class="font-weight-black">Facebook</span>
                </template>
              </v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col>
              <v-text-field outlined placeholder=" " hide-details>
                <template v-slot:label>
                  <span class="font-weight-black">Instagram</span>
                </template>
              </v-text-field>
            </v-col>
            <v-col>
              <v-text-field outlined placeholder=" " hide-details>
                <template v-slot:label>
                  <span class="font-weight-black">Twitter</span>
                </template>
              </v-text-field>
            </v-col>
          </v-row>
        </v-container> -->
        <v-text-field outlined>
          <template v-slot:label>
            <span class="font-weight-black">LinkedIn</span>
          </template>
        </v-text-field>
        <v-text-field outlined>
          <template v-slot:label>
            <span class="font-weight-black">Facebook</span>
          </template>
        </v-text-field>
        <v-text-field outlined>
          <template v-slot:label>
            <span class="font-weight-black">Instagram</span>
          </template>
        </v-text-field>
        <v-text-field outlined>
          <template v-slot:label>
            <span class="font-weight-black">Twitter</span>
          </template>
        </v-text-field>
      </div>
      <div class="d-flex flex-column">
        <div class="module-outcomes__actions">
          <div class="module-outcomes__actions-cancel text-button">
            <a href="">
              cancel
            </a>
          </div>
          <v-btn :ripple="false" height="40" outlined
          class="active module-outcomes__actions-save elevation-0">
            Save
          </v-btn>
        </div>
      </div>
    </div>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue';
import gql from 'graphql-tag';

export default Vue.extend({
  name: 'ModuleOutcomes',
  apollo: {
    goal: gql`query outcomeQuery{
      mApracticelogOpt{
        goal,
      }
    }`,
    minReq: gql`query outcomeQuery{
      mApracticelogOpt{
        minReq,
      }
    }`,
  },
  data: () => ({
    minutesReq: [
      '10m',
      '20m',
      '30m',
      '45m',
      '60m',
    ],
    minutesNec: [
      '100m',
      '200m',
      '300m',
      '400m',
      '500m',
      '600m',
      '700m',
      '800m',
      '900m',
      '1000m',
    ],
    minReq: 'Select',
    goal: 'Select',
  }),
});
</script>
