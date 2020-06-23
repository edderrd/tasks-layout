<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      mini-variant
      app
      clipped
      :class="appBarColor"
      class="darken-4"
    >
      <v-list dense>
        <template v-for="(link, index) in links">
          <v-list-item
            link
            :key="index"
            @click="setAppBarTitle(link.label, link.icon)"
          >
            <v-list-item-action>
              <v-icon>{{ link.icon }}</v-icon>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>{{ link.label }}</v-list-item-title>
            </v-list-item-content>
            <v-list-item-action v-if="link.due_count">
              <v-chip x-small color="red darken-3">{{ link.due_count }}</v-chip>
            </v-list-item-action>
          </v-list-item>
        </template>
      </v-list>
      <v-list dense subheader>
        <v-divider></v-divider>
        <template v-for="(project, index) in projects">
          <v-list-item
            link
            :key="index"
            @click="setAppBarTitle(project.label, null, project.color)"
          >
            <v-list-item-avatar>
              <v-avatar
                :size="28"
                class="text-uppercase body-2"
                :color="project.color"
                >{{ `${project.label[0]}${project.label[1]}` }}</v-avatar
              >
            </v-list-item-avatar>
            <v-list-item-content>
              <v-list-item-title>{{ project.label }}</v-list-item-title>
            </v-list-item-content>
            <v-list-item-action v-if="project.due_count">
              <v-chip x-small color="red darken-4">{{
                project.due_count
              }}</v-chip>
            </v-list-item-action>
          </v-list-item>
        </template>
        <v-list-item link>
          <v-list-item-action>
            <v-icon color="grey">mdi-plus</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title class="grey--text"
              >Add a project...</v-list-item-title
            >
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <template #append>
        <div class="mb-5 d-flex justify-center align-center">
          <v-btn icon>
            <v-avatar :size="26">
              <img src="//www.gravatar.com/avatar/none?f=y&d=mm" />
            </v-avatar>
          </v-btn>
        </div>
      </template>
    </v-navigation-drawer>
    <v-content>
      <div style="display: flex; min-height: min-content;">
        <div style="height: 99.8vh; overflow: auto;">
          <v-navigation-drawer
            width="380px"
            :class="appBarColor"
            class="darken-3"
          >
            <v-toolbar
              :class="appBarColor"
              class="darken-3"
              flat
              :extended="isSearching"
              style="position: sticky; top: 0; z-index: 1; margin-right: 1px;"
            >
              <v-toolbar-title>
                {{ appBarTitle }}
              </v-toolbar-title>
              <v-spacer></v-spacer>
              <v-btn icon @click="isSearching = !isSearching">
                <v-icon>mdi-magnify</v-icon>
              </v-btn>
              <v-btn icon>
                <v-icon>mdi-plus</v-icon>
              </v-btn>
              <template #extension v-if="isSearching">
                <v-text-field
                  autofocus
                  style="margin-bottom: -25px"
                  class="mr-2"
                  prepend-inner-icon="mdi-magnify"
                  clearable
                  rounded
                  filled
                  solo
                  flat
                  dense
                  @keydown.esc="isSearching = false"
                  placeholder="Search"
                ></v-text-field>
              </template>
            </v-toolbar>
            <v-list subheader two-line>
              <v-subheader>In Process</v-subheader>
              <draggable v-model="issues">
                <v-list-item link v-for="(issue, index) in issues" :key="index">
                  <v-list-item-content>
                    <v-list-item-title>{{
                      `${issue.title} ${index}`
                    }}</v-list-item-title>
                    <v-list-item-subtitle>{{
                      issue.description
                    }}</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
              </draggable>
            </v-list>
            <v-list subheader two-line>
              <v-subheader>To Do</v-subheader>
              <draggable v-model="issues">
                <v-list-item link v-for="(issue, index) in issues" :key="index">
                  <v-list-item-content>
                    <v-list-item-title>{{
                      `${issue.title} ${index}`
                    }}</v-list-item-title>
                    <v-list-item-subtitle>{{
                      issue.description
                    }}</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
              </draggable>
            </v-list>
          </v-navigation-drawer>
        </div>
        <div style="height: 99.8vh; overflow: auto;" id="main-content">
          <Home />
        </div>
      </div>
    </v-content>
  </v-app>
</template>

<script>
import draggable from "vuedraggable";
import Home from "./components/Home";

export default {
  name: "App",

  components: {
    draggable,
    Home
  },

  data: () => ({
    drawer: true,
    appBarColor: "grey",
    appBarTitle: "Tasks",
    appBarIcon: "mdi-lightbulb",
    isSearching: false,
    links: [
      { label: "Inbox", icon: "mdi-inbox", color: "background" },
      {
        label: "Planned",
        icon: "mdi-clock-outline",
        due_count: 2,
        color: "background"
      }
    ],
    projects: [
      { label: "Accounting", color: "cyan", due_count: 1 },
      { label: "Secret Game", color: "green" },
      { label: "Dashboard", color: "blue", due_count: 1 }
    ],
    issues: [
      {
        title: "some random title",
        order: 1,
        description: "Lorem, ipsum dolor sit amet"
      },
      {
        title: "some random title",
        order: 2,
        description: "Lorem, ipsum dolor sit amet"
      },
      {
        title: "some random title",
        order: 3,
        description: "Lorem, ipsum dolor sit amet"
      },
      {
        title: "some random title",
        order: 3,
        description: "Lorem, ipsum dolor sit amet"
      },
      {
        title: "some random title",
        order: 3,
        description: "Lorem, ipsum dolor sit amet"
      },
      {
        title: "some random title",
        order: 3,
        description: "Lorem, ipsum dolor sit amet"
      },
      {
        title: "some random title",
        order: 3,
        description: "Lorem, ipsum dolor sit amet"
      },
      {
        title: "some random title",
        order: 3,
        description: "Lorem, ipsum dolor sit amet"
      },
      {
        title: "some random title",
        order: 3,
        description: "Lorem, ipsum dolor sit amet"
      },
      {
        title: "some random title",
        order: 3,
        description: "Lorem, ipsum dolor sit amet"
      },
      {
        title: "some random title",
        order: 4,
        description: "Lorem, ipsum dolor sit amet"
      }
    ]
  }),

  created() {
    this.$vuetify.theme.dark = true;
  },

  methods: {
    setAppBarTitle(title, icon, color = "grey") {
      this.appBarColor = color;
      this.appBarTitle = title;
      this.appBarIcon = icon;
    }
  }
};
</script>
