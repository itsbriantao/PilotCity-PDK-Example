<template>
  <v-container class="module-default">
    <div class="module-default__instructions">
      <v-expansion-panels class="module-default__instructions" flat v-model="showInstructions">
        <v-expansion-panel>
          <v-expansion-panel-header v-show="showInstructions" @click="showInstructions = false"
          hide-actions class="pa-0">
            <template v-slot="{open}">
              <v-scroll-y-transition hide-on-leave>
                <div v-if="!open" class="d-flex flex-column justify-center">
                  <v-icon  class="d-flex justify-center secondary--text">
                    mdi-chevron-down
                  </v-icon>
                  <div
                  class="text-uppercase
                  font-weight-bold text-subtitle-2
                  secondary--text text-center">
                      Instructions
                  </div>
                </div>
              </v-scroll-y-transition>
            </template>
          </v-expansion-panel-header>
          <v-expansion-panel-content>
            <module-instruct readonly/>
            <div @click="showInstructions = true">
              <div class="text-uppercase
              font-weight-bold text-subtitle-2
              secondary--text text-center">
                close
              </div>
              <div class="hr"/>
              <v-icon class="d-flex secondary--text justify-center">
                mdi-chevron-up
              </v-icon>
            </div>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </div>
    <!-- TODO: # validation -->
    <!-- <v-text-field outlined placeholder="##m" class="module-default__input-text">
      <template v-slot:label>
        <span class="font-weight-black black--text">Enter Minutes</span>
      </template>
    </v-text-field>
    <v-btn block outlined :ripple="false"
    class="module-default__input-btn
    font-weight-black black--text">
      Log Minutes
    </v-btn>
    <span class="module-default__caption
    text-uppercase font-weight-black text-caption">
    logged minutes
    </span>
    <span class="font-weight-black text-h4 module-default__time">
      143h 58m
    </span> -->
      <v-container class="module-edit my-7">
        <div class="module-edit__container">
          <v-row><p class="text-h5 font-weight-black">{{ employerName }} RFP</p></v-row>
          <v-row><p class="text-h6 font-italic">{{ headline }}</p></v-row>
          <v-row><span class="text-h6 font-weight-black">Prompt</span></v-row>
          <v-row><p class="text-h6">{{ prompt }}</p></v-row>
          <v-row><span class="text-h6 font-weight-black">Requirements</span></v-row>
          <v-row><ul>
            <li class="text-h6" v-for="req in requirements" :key="req">{{ req }}</li>
          </ul></v-row>
          <br>
          <v-row><span class="text-h6 font-weight-black">About {{ employerName }}</span></v-row>
          <v-row><p class="text-h6">{{ about }}</p></v-row>
          <v-row><span class="text-h6 font-weight-black">Social</span></v-row>
          <v-row><ul>
            <li class="text-h6" v-for="s in social" :key="s" v-html="s"></li>
          </ul></v-row>
          <br>
          <v-row><span class="text-h6 font-weight-black">Resources</span></v-row>
          <v-row><ul>
            <li class="text-h6" v-for="resource in resources"
            :key="resource" v-html="resource"></li>
          </ul></v-row>
          <br>
          <v-row justify="center">
            <v-checkbox v-model="checkbox">
              <template v-slot:label>
                <div class="text-body-1 font-weight-black">
                  I have fully read and understand the RFP.
                </div>
              </template>
            </v-checkbox>
          </v-row>
        </div>
      </v-container>
      <v-btn outlined :ripple="false"
      class="module-default__btn
      font-weight-black black--text">
        Next
      </v-btn>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue';
import Instruct from './ModuleInstruct.vue';
import Edit from './ModuleEdit.vue';

export default Vue.extend({
  name: 'ModuleDefault',
  components: {
    'module-instruct': Instruct,
  },
  data: () => ({
    showInstructions: true,
    employerName: 'PhaseSpace',
    headline: '3D design a commercially viable VR training experience to increase immersive, real-time learning in an industry of your choice.',
    prompt: 'Use PhaseSpace’s motion capturing platform to conceptualize solutions for virtual reality training in industries that require simulation to best train their human resources to increase the quality of delivery and execution.',
    requirements: ['Prototype must utilize the PhaseSpace motion sensor system', 'Prototype must cost less than $100 to produce'],
    about: 'PhaseSpace has always been dedicated to the mission of developing new technologies and products for the exploding motion capture and motion tracking markets. We have developed motion capture solutions for academic and medical research, training simulations, robotics, graphic arts, and entertainment industries.',
    social: [
      'Website'.link('https://www.phasespace.com'),
      'LinkedIn'.link('https://www.linkedin.com/company/phasespace-inc./?trk=company_logo'),
      'Twitter'.link('https://twitter.com/PhaseSpaceMocap'),
    ],
    resources: [
      'https://www.google.com'.link('https://www.google.com'),
      'https://www.pilotcity.com/library/phasespace-rfp'.link('https://www.google.com'),
    ],
  }),
  created() {
    console.log(Edit);
  },
});
</script>
