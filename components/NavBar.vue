<template>
  <div style="padding-bottom: 20px">
    <b-navbar toggleable="lg" type="light">
      <b-navbar-brand>
        <img src="~/assets/images/kf.png" height="70" width="120" alt="" />
      </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="/">Home</b-nav-item>
          <b-nav-item href="/">Gallery</b-nav-item>
          <b-nav-item href="/">Rent </b-nav-item>
          <b-nav-item href="/">Buy </b-nav-item>
          <b-button
            @click="revokeAuthentication()"
            style="background-color: transparent; border: none"
            >Logout</b-button
          >
        </b-navbar-nav>
        <!-- <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown style="color: #160d3d" right>
            <template #button-content>
              <em>
                <b-avatar variant="light"></b-avatar>
              </em>
            </template>
            <b-dropdown-item class="heading4" href="/profile">Profile</b-dropdown-item>
            <b-dropdown-item class="heading4" href="/">Logout</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav> -->
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
export default {
  head: {
    title: "Home",
    script: [
      {
        src: "https://cdnjs.cloudflare.com/ajax/libs/jquery/3.1.1/jquery.min.js",
      },
      { src: "//ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js" },
    ],
    link: [
      {
        rel: "stylesheet",
        href: "https://fonts.googleapis.com/css?family=Roboto&display=swap",
      },
    ],
  },

  computed: {
    ...mapState({
      isAuthenticated: "isAuthenticated",
      loggedinUserName: "loggedinUserName",
      loggedinUserPhone: "loggedinUserPhone",
    }),
  },
  methods: {
    ...mapActions({
      peristAuthentication: "peristAuthentication",
      peristUserPhone: "peristUserPhone",
      peristUserName: "peristUserName",
    }),
    async revokeAuthentication() {
      await this.peristAuthentication(false);
      await this.peristUserPhone("");
      await this.peristUserName("");
      return this.$router.push("/login");
    },
  },
};
</script>
