<template>
  <div class="page-options flex h-100">
    <aside :class="{ 'show-aside': aside }">
      <div class="aside-content">
        <img src="/public/images/icon128.png">
        <h1 v-text="i18n('extName')"></h1>
        <div class="aside-menu">
          <a href="#scripts" :class="{active: tab === 'scripts'}" v-text="i18n('sideMenuInstalled')"></a>
          <a href="#settings" :class="{active: tab === 'settings'}" v-text="i18n('sideMenuSettings')"></a>
          <a href="#privacySettings" :class="{active: tab === 'privacySettings'}" v-text="i18n('Privacy Settings')"></a>
          <a href="#about" :class="{active: tab === 'about'}" v-text="i18n('sideMenuAbout')"></a>
        </div>
        <div class="aside-toggle visible-sm" @click="aside = !aside">
          <icon name="arrow" />
        </div>
      </div>
    </aside>
    <component :is="tabComponent" class="tab flex-auto"></component>
  </div>
</template>

<script>
import Icon from '#/common/ui/icon';
import { store } from '../utils';
import Installed from './tab-installed';
import Settings from './tab-settings';
import PrivacySettings from './tab-privacy-settings';
import About from './tab-about';

const tabs = {
  scripts: Installed,
  settings: Settings,
  privacySettings: PrivacySettings,
  about: About,
};

export default {
  components: {
    Icon,
  },
  data() {
    return {
      aside: false,
      store,
    };
  },
  computed: {
    tab() {
      let tab = this.store.route.paths[0];
      if (!tabs[tab]) tab = 'scripts';
      return tab;
    },
    tabComponent() {
      return tabs[this.tab];
    },
  },
};
</script>

<style src="../style.css"></style>
