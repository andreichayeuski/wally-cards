<template>
  <div class="page">
    <Header title="Интеграции" description="Активные и неактивные интеграции" />
    <div class="page-content integrations">
      <h3>Активные интеграции ({{ activeCount }})</h3>
      <IntegrationsBlock
        v-show="activeCount > 0"
        :servicesList="activeIntegrations"
        class="active-integrations"
      />
      <h3>Неактивные интеграции ({{ disabledCount }})</h3>
      <IntegrationsBlock
        v-show="disabledCount > 0"
        :servicesList="disabledIntegrations"
        class="disabled-integrations"
      />
    </div>
  </div>
</template>

<script>
import Header from "../../common/Header.vue";
import IntegrationsBlock from "./IntegrationsBlock.vue";

export default {
  name: "Integrations",
  components: {
    Header,
    IntegrationsBlock,
  },
  data() {
    return {
      some: false,
    };
  },
  computed: {
    activeIntegrations: function () {
      return this.$store.state.integrations.filter((x) => x.enabled);
    },
    disabledIntegrations: function () {
      return this.$store.state.integrations.filter((x) => !x.enabled);
    },
    activeCount: function () {
      return this.activeIntegrations.length;
    },
    disabledCount: function () {
      return this.disabledIntegrations.length;
    },
  },
};
</script>