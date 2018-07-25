<template>
  <div id="app">
    <b-navbar toggleable="md" type="light" variant="light">
      <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>
      <b-navbar-brand href="#">Zerch</b-navbar-brand>
    </b-navbar>

    <div class="container-fluid">
      <div class="row mx-auto">
        <!-- Search input section -->
        <section class="col-sm-12 pt-3 px-0">
          <vs-input @search="onSearch"></vs-input>
        </section>
        <!-- Results section -->
        <section class="results">
          <vs-results :data="results"></vs-results>
        </section>
      </div>
    </div>
</div>
</template>

<script lang="ts">
import { Component, Vue, Prop, Provide } from 'vue-property-decorator'
import VsResults from './search-results/vs-results.vue';
import VsInput from './search-input/vs-input.vue';
import voyagerApi from './search-results/search-api';

@Component({
  components: {
    VsResults,
    VsInput
  }
})
export default class App extends Vue {

  @Provide() 
  results = [];

  async onSearch(term) {
    this.results = await voyagerApi.search(term);
  }
}

</script>

<style lang="scss">
  #app {
    color: #56b983;
  }
</style>
