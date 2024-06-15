<template>
  <v-app>
    <v-app-bar color="indigo" dark app>
      <v-toolbar-title>求人情報</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <v-btn text to="/">ホーム</v-btn>
        <v-btn text to="/editor">仕事追加</v-btn>
      </v-toolbar-items>
    </v-app-bar>
    <v-main>
      <router-view />
    </v-main>
    <v-footer color="grey" dark app class="justify-center">
      Django Startup - Step3
    </v-footer>
  </v-app>
</template>
