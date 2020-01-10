<template>
  <div style="position: relative;">
    <v-toolbar
      style="position: sticky; top: 0; z-index: 1"
      color="background"
      :flat="!contentScrolled"
    >
      <v-toolbar-title>Some random title 1</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>mdi-clock</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>mdi-settings</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>mdi-menu</v-icon>
      </v-btn>
    </v-toolbar>
    <div class="pa-4" v-scroll:#main-content="onScroll">
      <v-card>
        <v-card-text
          class="grey--text text--lighten-2"
        >Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quisquam alias a aliquam recusandae quia maxime accusantium natus blanditiis perspiciatis unde! Ad aspernatur nulla tempora facere corrupti animi labore iure. Sapiente?</v-card-text>
      </v-card>

      <div class="mt-6">
        <v-subheader class="ml-0 pl-0">Comments</v-subheader>
        <v-card v-for="(comment, index) in comments" :key="index" class="mb-4">
          <v-list>
            <v-list-item>
              <v-list-item-action>
                <v-avatar :size="26" color="primary">ME</v-avatar>
              </v-list-item-action>
              <v-list-item-content
                class="body-2 grey--text text--lighten-2"
              >Comment {{ index }}: Lorem ipsum dolor sit amet consectetur adipisicing elit. Ad quod iste laudantium possimus cupiditate reprehenderit. Deleniti facere culpa ut libero quod, nihil ea quo similique vitae, id quas nesciunt ducimus.</v-list-item-content>
            </v-list-item>
          </v-list>
        </v-card>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",

  data: () => ({
    comments: new Array(40),
    contentScrolled: false
  }),

  methods: {
    onScroll(e) {
      this.contentScrolled = e.target.scrollTop >= 1;
    }
  }
};
</script>
