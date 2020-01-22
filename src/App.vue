<template>
  <div id="app">
    <div class="container">
      <h1 class="mt-3">Insane profile card generator</h1>
      <div class="d-flex justify-content-center mt-auto" v-if="!profiles.length" style="height: 500px;">
        <button class="btn btn-executive btn-outline btn-lg" type="button" @click="openSheet">
          <i class="material-icons">add</i>
          Create your first profile card!</button>
      </div>
      <div v-else>
        <button class="btn-lg btn noprint mb-2" onclick="window.print();return false;">Print</button>
        <div class="d-flex flex-row flex-wrap">
          <div v-for="(profile, index) in profiles" :key="`profile-${index}`" :theme="profile.theme">
            <profile-card class="my-2 mr-3" :avatar="profile.avatar" :icons="profile.icons" :name="profile.name"
              :email="profile.email" :role="profile.role" :bio="profile.bio" :theme="profile.theme" />
            <div class="noprint d-flex justify-content-center">
              <button class="btn btn-destructive noprint" @click="profiles.splice(index, 1)">Delete {{ profile.name }}</button>
            </div>
          </div>

        </div>
        <div class="d-flex justify-content-center my-5 noprint" style="height: 200px" v-if="profiles.length < 4">
          <button class="btn btn-executive btn-outline btn-lg noprint" type="button" @click="openSheet">
            <i class="material-icons">add</i>
            Create another card!</button>
        </div>
        <h2 v-else class="noprint">Max 4 cards for now</h2>
      </div>

      <profile-sheet v-model="profiles" />

    </div>
  </div>
</template>

<script>
  import ProfileCard from "./components/Card";
  import ProfileSheet from "./components/Sheet";
  export default {
    name: 'app',
    components: {
      ProfileCard,
      ProfileSheet
    },
    data: () => {
      return {
        profiles: []
      };
    },
    mounted() {
      window.dg.sheet.init();
    },
    methods: {
      openSheet() {
        window.dg.sheet.init();
        window.dg.sheet.open("profile-sheet");
      }
    }
  }
</script>

<style>
  @media print {
    .noprint {
      display: none;
    }
  }
</style>