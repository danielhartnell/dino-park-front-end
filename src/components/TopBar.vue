<template>
  <header class="top-bar">
    <div class="top-bar__bar">
      <router-link :to="{ name: 'Home' }" class="top-bar__link top-bar__link--logo"><img src="@/assets/images/mozilla.svg" alt="Mozilla logo" width="90" /></router-link>
      <SearchForm class="hide-mobile"></SearchForm>
      <button class="hide-desktop top-bar__search-toggle" @click="toggleMobileSearch" aria-controls="mobile-search" :aria-expanded="mobileSearchOpen ? 'true' : 'false'">
        <img src="@/assets/images/search.svg" alt="" role="presentation" aria-hidden="true" width="20" />
        <span class="visually-hidden">
          <template v-if="mobileSearchOpen">Hide search</template>
          <template v-else>Show search</template>
        </span>
      </button>
      <router-link :to="{ name: 'Orgchart' }" class="top-bar__link" exact-active-class="top-bar__link--current"><img src="@/assets/images/org-chart.svg" alt="Org chart" width="20" /></router-link>
      <ShowMore buttonText="Open user menu" alternateButtonText="Close user menu" buttonClass="top-bar__user-menu-toggle" :expanded="false" v-on:close-user-menu="closeUserMenu()" ref="showMoreEl">
        <template slot="overflow">
          <UserMenu></UserMenu>
        </template>
        <template slot="button-content">
          <img src="@/assets/images/user-demo.png" alt="Avatar" width="40" />
        </template>
      </ShowMore>
    </div>
    <SearchForm modifier="search-form--small hide-desktop" v-if="mobileSearchOpen" id="mobile-search"></SearchForm>
  </header>
</template>

<script>
import SearchForm from '@/components/SearchForm.vue';
import ShowMore from '@/components/functional/ShowMore.vue';
import UserMenu from '@/components/UserMenu.vue';

export default {
  name: 'TopBar',
  components: {
    SearchForm,
    ShowMore,
    UserMenu,
  },
  methods: {
    closeUserMenu() {
      this.$refs.showMoreEl.expanded = false;
    },
    toggleMobileSearch() {
      this.mobileSearchOpen = !this.mobileSearchOpen;
    },
  },
  data() {
    return {
      searchQuery: '',
      mobileSearchOpen: false,
    };
  },
};
</script>

<style>
  .top-bar__bar {
    background-color: var(--white);
    border-bottom: 1px solid var(--gray-30);
    display: flex;
    align-items: center;
    margin-bottom: 2em;
    position: fixed;
    width: 100%;
    top: 0;
    padding: .25em;
    z-index: var(--layerTopBar);
  }
    .top-bar__search-toggle {
      border: 0;
      background-color: transparent;
      padding: 1em;
      line-height: 0;
    }
    .top-bar__search-toggle[aria-expanded="true"] {
      background-color: var(--gray-20);
    }
    .top-bar__link {
      padding: 1.25em;
      text-transform: uppercase;
      font-size: .9em;
      color: var(--black);
      font-weight: 700;
      text-decoration: none;
    }
    .top-bar__link img {
      vertical-align: middle;
    }
    .top-bar__link--current  {
      position: relative;
    }
    .top-bar__link--current::after {
      content: '';
      height: 2px;
      background: black;
      width: 100%;
      position: absolute;
      bottom: -.5em;
      left: 0;
    }
    .top-bar__link--logo {
      margin-right: auto;
      margin-left: 0;
      padding: 1em;
      max-width: none; /* don't shrink on small screens */
    }
    .top-bar__link--logo img {
      vertical-align: middle;
    }
    .top-bar .show-more {
      padding: .5em 1em;
    }
    .top-bar__user-menu-toggle {
      border: 0;
      background-color: none;
      padding: 0;
    }
      .top-bar__user-menu-toggle .show-more__button-text {
        position: absolute;
        left: -9999em;
        top: -9999em;
      }
</style>
