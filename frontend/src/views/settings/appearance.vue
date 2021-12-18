<template>
  <div class="items">
    <b-tabs :animated="false" v-model="activeTab">
      <b-tab-item :label="$t('settings.appearance.admin.name')" label-position="on-border">
        <div class="block">
          {{ $t('settings.appearance.admin.help') }}
        </div>

        <b-field :label="$t('settings.appearance.customCSS')" label-position="on-border">
          <html-editor v-model="data['appearance.admin.custom_css']" name="body"
          language="css" />
        </b-field>
      </b-tab-item><!-- admin -->

      <b-tab-item :label="$t('settings.appearance.public.name')" label-position="on-border">
        <div class="block">
          {{ $t('settings.appearance.public.help') }}
        </div>

        <b-field :label="$t('settings.appearance.customCSS')" label-position="on-border">
          <html-editor v-model="data['appearance.public.custom_css']" name="body"
          language="css" />
        </b-field>

        <b-field :label="$t('settings.appearance.customJS')" label-position="on-border">
          <html-editor v-model="data['appearance.public.custom_js']" name="body"
          language="js" />
        </b-field>
      </b-tab-item><!-- public -->
    </b-tabs>
  </div>
</template>

<script>
import Vue from 'vue';
import { mapState } from 'vuex';
import HTMLEditor from '../../components/HTMLEditor.vue';

export default Vue.extend({
  components: {
    'html-editor': HTMLEditor,
  },

  props: {
    form: {
      type: Object,
    },
  },

  data() {
    return {
      data: this.form,
      activeTab: 0,
    };
  },

  watch: {
    activeTab: function activeTab() {
      localStorage.setItem('admin.settings.appearance.active_tab', this.activeTab);
    },
  },

  mounted() {
    // Reload active tab.
    if (localStorage.getItem('admin.settings.appearance.active_tab')) {
      this.activeTab = JSON.parse(localStorage.getItem('admin.settings.appearance.active_tab'));
    }
  },

  computed: {
    ...mapState(['settings']),
  },
});

</script>
