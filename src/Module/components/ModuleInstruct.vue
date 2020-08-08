<template>
<!--  TODO: make the inputs into actual components -->
  <v-container class="module-instruct">
    <div class="module-instruct__container">
      <div class="module-instruct__description">
        <div class="module-instruct__description-label
        font-weight-black text-subtitle-2 text-uppercase">
          <span>Instructions</span>
        </div>
        <div :contenteditable=!readonly @input="updateDesc" class="font-weight-black text-body-1">
          {{moduleDescription}}
        </div>
      </div>
      <div class="module-instruct__instructions">
        <div class="module-instruct__instructions-item"
        v-for="(item, index) in instructions" :key="item">
          <v-avatar size="35" class="module-instruct__instructions-av
          font-weight-black text-caption d-none d-sm-flex">
            {{ index+1 }}
          </v-avatar>
          <div :contenteditable=!readonly @input="updateItem($event, index)"
          class="module-instruct__instructions-text font-weight-black text-body-1">
            {{ item }}
          </div>
        </div>
        <div @click="addItem"
        v-if="!readonly"
        class="module-instruct__instructions-add
        font-weight-black text-body-1">
          <v-icon class="module-instruct__instructions-add-icon">
            mdi-plus
          </v-icon>
        </div>
      </div>
      <div class="d-flex flex-column">
        <div v-if="!readonly" class="module-instruct__actions">
          <div class="module-instruct__actions-cancel text-button">
            <span href="">cancel</span>
          </div>
          <v-btn :ripple="false" height="40" outlined
          class="active module-instruct__actions-save elevation-0">
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
  name: 'ModuleInstruct',
  props: {
    readonly: {
      type: Boolean,
      default: false,
    },
  },
  apollo: {
    instructions: gql`query instructQuery{
      mApracticelogOpt{
        instructions
      }
    }`,
  },
  data: () => ({
    moduleDescription: 'The Request for Pilot (RFP) is a document meant to introduce the student to the project they have chosen.',
    instructions: [
      'Read all sections of the RFP to make sure you understand the problem and the project.',
      'Do research on the problem and brainstorm your idea.',
      'Complete all the deliverables in this program to auto-apply for your internship.',
    ], // TODO: parse for empty string (strings w/o _real_ characters)
  }),
  methods: {
    updateDesc(e: Event) {
      const el = e.target as HTMLTextAreaElement;
      this.moduleDescription = el.innerText;
      console.log('description has been updated!');
    },
    updateItem(e: Event, i: number) {
      const el = e.target as HTMLTextAreaElement;
      this.instructions[i] = el.innerText;
      console.log(`instruction ${i} has been updated!`);
    },
    addItem() {
      this.instructions.push('');
    },
  },
});
</script>
