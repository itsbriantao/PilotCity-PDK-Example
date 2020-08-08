<template>
<v-container class="module-edit">
  <!-- <div class="module-edit__container">
    <div class="module-edit__title">
      <div class="text-subtitle-2 time font-weight-black text-capitalize">Time</div>
      <div class="text-subtitle-2 name font-weight-black text-capitalize">Name</div>
    </div>
    <div class="module-edit__user" v-for="user in users" :key="user.name">
      <div class="module-edit__user-time text-h6 font-weight-black">
        {{`${user.totalTime}m`}}
      </div>
      <div class="module-edit__user-data">
        <div class="module-edit__user-name text-h6 font-weight-black">
          {{user.name}}
        </div>
        <div class="module-edit__user-entry text-subtitle-2 font-weight-black"
        v-for="(entry,index) in user.entries" :key="entry+index">
          <div class="module-edit__user-entry-action">
            <v-btn outlined small class="rounded-0"
            :class="{'rejected':entry.status=='accepted', 'accepted':entry.status=='rejected'}"
            width="80.2">
              {{entry.status=='accepted'?'reject':'accept'}}
              </v-btn>
          </div>
          <div class="module-edit__user-entry-time">
            <span>{{`${entry.time}m`}}</span>
          </div>
        </div>
      </div>
    </div>
  </div> -->
  <div class="module-edit__container">
    <!-- Headline -->
    <v-row>
      <span class="module-edit__title text-h5 font-weight-black">
        {{ headline.title }}
      </span>
    </v-row>
    <v-row><p>{{ headline.description }}</p></v-row>
    <v-row>
      <v-text-field
        autofocus
        outlined
        :placeholder="headline.placeholder"
        v-model="headline.content">
      </v-text-field>
    </v-row>
    <!-- Prompt -->
    <v-row>
      <span class="module-edit__title text-h5 font-weight-black">
        {{ prompt.title }}
      </span>
    </v-row>
    <v-row><p v-html="prompt.description"></p></v-row>
    <v-row>
      <v-textarea
        auto-grow
        outlined
        :placeholder="prompt.placeholder"
        v-model="prompt.content">
      </v-textarea>
    </v-row>
    <!-- Requirements -->
    <v-row>
      <span class="module-edit__title text-h5 font-weight-black">
        {{ reqs.title }}
      </span>
    </v-row>
    <v-row><p v-html="reqs.description"></p></v-row>
    <v-row v-for="(req, index) in reqs.content" :key="index">
      <v-text-field
      dense
      outlined
      :placeholder="reqs.placeholder"
      v-model="reqs.content[index]"
      :value="req">
      </v-text-field>
    </v-row>
    <!-- <v-row v-for="n in 3" :key="n">
      <v-text-field
      dense
      outlined
      :placeholder="req.placeholder"
      :value="`Testing ${n}`">
      </v-text-field>`
    </v-row> -->
    <v-row>
      <div @click="addItem"
      class="module-instruct__instructions-add
      font-weight-black text-body-1">
        <v-icon class="module-instruct__instructions-add-icon">
          mdi-plus
        </v-icon>
      </div>
    </v-row>
    <!-- <div class="module-instruct__instructions-item"
    v-for="(item, index) in req.content" :key="item">
      <div @input="updateItem($event, index)"
      class="module-instruct__instructions-text font-weight-black text-body-1">
        {{ item }}
      </div>
    </div> -->
    <!-- About -->
    <v-row class="mt-7">
      <span class="module-edit__title text-h5 font-weight-black">
        {{ about.title }}
      </span>
    </v-row>
    <v-row><p>{{ about.description }}</p></v-row>
    <v-row>
      <v-textarea auto-grow outlined :placeholder="about.placeholder"></v-textarea>
    </v-row>
    <!-- Resources -->
    <v-row>
      <span class="module-edit__title text-h5 font-weight-black">
        {{ resources.title }}
      </span>
    </v-row>
    <v-row><p>{{ resources.description }}</p></v-row>
    <v-row>
      <v-textarea auto-grow outlined :placeholder="resources.placeholder"></v-textarea>
    </v-row>
    <!-- Cancel and Save buttons -->
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

export default Vue.extend({
  name: 'ModuleEdit',
  data: () => ({
    headline: {
      title: 'Project Headline',
      description: 'Keep the headline concise but descriptive. It’s the first thing students will read.',
      placeholder: 'Type in your headline here.',
      content: null,
    },
    prompt: {
      title: 'Project Prompt',
      description: `Describe their mission. Here's a simple template: Use (a product or service) to conceptualize,
        design or prototype (a solution) that solves (a problem or opportunity) to reach (a key metric).
        <br><br>
        Need some direction in writing this? Click <a href="https://www.pilotcity.com/library/how-do-i-decide-on-my-project-for-students">here</a>
        to check out our handy guide in crafting a prompt.`,
      placeholder: 'Type in your prompt here.',
      content: null,
    },
    reqs: {
      title: 'Project Requirements',
      description: `The following specifications are parameters in which students must design, prototype and
        develop their project to meet employer requirements. 
        <br><br>
        Read <a href="https://www.pilotcity.com/library/why-are-employer-specifications-for-the-project-important">more</a>
        on why the employer's specifications are important.`,
      placeholder: 'Type in your requirements here.',
      content: [
        'Prototype must utilize the PhaseSpace motion sensor system',
        'Prototype must cost less than $100 to produce',
      ],
    },
    about: {
      title: 'About Us',
      description: 'Offer an overview of your company, such as what you do, what your mission is, what your values are, where you are based, etc.',
      placeholder: 'Type in your overview here.',
      content: null,
    },
    resources: {
      title: 'Resources',
      description: 'Offer some resources for the student to help them learn more about your product and their project. This can be links to articles, videos, or just general advice.',
      placeholder: 'Offer some resources here.',
      content: null,
    },
  }),
  methods: {
    // updateDesc(e: Event) {
    //   const el = e.target as HTMLTextAreaElement;
    //   this.moduleDescription = el.innerText;
    //   console.log('description has been updated!');
    // },
    // updateItem(e: Event, i: number) {
    //   const el = e.target as HTMLTextAreaElement;
    //   this.instructions[i] = el.innerText;
    //   console.log(`instruction ${i} has been updated!`);
    // },
    addItem() {
      const reqArray = this.reqs.content;
      // If the latest requirement textfield is not empty
      if (reqArray[reqArray.length - 1] !== '') {
        reqArray.push('');
      }
      // TODO: bring focus to the empty textfield
    },
  },
});
</script>
