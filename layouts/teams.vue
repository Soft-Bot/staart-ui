<template>
  <div class="has-background-white-bis">
    <Navbar />
    <div class="container">
      <div class="columns">
        <aside class="column">
          <b-menu :activable="false">
            <b-menu-list>
              <b-menu-item
                v-for="(item, i) in items"
                :key="`i${i}${item.to}`"
                :icon="item.icon"
                :label="item.label"
                tag="router-link"
                :to="`/teams/${$route.params.username}${item.to}`"
                :active="
                  $route.path === `/teams/${$route.params.username}${item.to}`
                "
                :expanded="
                  $route.path.includes(
                    `/teams/${$route.params.username}${item.to}`
                  )
                "
              >
                <b-menu-item
                  v-for="(item, i) in item.items"
                  :key="`i${i}${item.to}`"
                  :icon="item.icon"
                  :label="item.label"
                  tag="router-link"
                  :to="`/teams/${$route.params.username}${item.to}`"
                  :active="
                    $route.path === `/teams/${$route.params.username}${item.to}`
                  "
                />
              </b-menu-item>
            </b-menu-list>
          </b-menu>
        </aside>
        <main class="column is-three-quarters card">
          <div class="card-content">
            <nuxt />
          </div>
        </main>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import Component from "vue-class-component";
import Navbar from "@/components/layout/Navbar.vue";
import Footer from "@/components/layout/Footer.vue";

@Component({
  components: { Navbar, Footer },
})
export default class Default extends Vue {
  items = [
    {
      label: "Dashboard",
      icon: "shape",
      to: "",
    },
    {
      label: "Settings",
      icon: "cog",
      to: "/settings",
      items: [
        {
          label: "Team settings",
          icon: "account-cog",
          to: "/settings/team",
        },
        {
          label: "Domains",
          icon: "web",
          to: "/settings/domains",
        },
      ],
    },
    {
      label: "Team members",
      icon: "account-group",
      to: "/members",
    },
    {
      label: "Billing",
      icon: "credit-card-multiple",
      to: "/billing",
      items: [
        {
          label: "Customer details",
          icon: "office-building",
          to: "/billing",
        },
        {
          label: "Subscription",
          icon: "history",
          to: "/billing/subscription",
        },
        {
          label: "Payment methods",
          icon: "credit-card",
          to: "/billing/sources",
        },
        {
          label: "Invoices",
          icon: "book-multiple",
          to: "/billing/invoices",
        },
        {
          label: "Credits & history",
          icon: "cash-plus",
          to: "/billing/transactions",
        },
      ],
    },
    {
      label: "Developers",
      icon: "code-braces",
      to: "/developers",
      items: [
        {
          label: "API keys",
          icon: "api",
          to: "/developers/api-keys",
        },
        {
          label: "Logs",
          icon: "chart-areaspline-variant",
          to: "/developers/api-logs",
        },
        {
          label: "Webhooks",
          icon: "webhook",
          to: "/developers/webhooks",
        },
      ],
    },
    {
      label: "Data and security",
      icon: "database",
      to: "/security",
    },
  ];
}
</script>

<style scoped>
.container {
  position: relative;
  margin-top: 2rem;
  z-index: 31;
  max-width: 1000px;
}
</style>

<style>
.is-transparent {
  background-color: transparent;
}
</style>
