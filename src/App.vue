<template>
  <div id="app">
    <nav>
      <router-link to="/">
        <div class="navigation__logo">
          Twotter
        </div>
      </router-link>
      <div class="navigation__user" v-if="user">
        {{ user.username }}
      </div>
    </nav>
    <router-view/>
  </div>
</template>

<script>
//import { reactive } from 'vue';
import { useStore } from 'vuex';
import { computed } from 'vue';

export default {
  name: 'App',
  setup() {
    const store = useStore();
    const user = computed(() => store.state.user);

    return {
      user
    }
  }
  /*
  setup() {
    const state = reactive({
      user: {
        username: 'Fizzecc'
      }
    })
    return {
      state
    }
  }
   */

}
</script>

<style lang="scss">
@font-face {
  font-family: "OpenSans-Regular";
  src: local("OpenSans-Regular"),
  url(./styles/fonts/Open_Sans/OpenSans-Regular.ttf) format("truetype");
}

#app{
  font-family: "OpenSans-Regular", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #F3F5FA;

  nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 5%;
    background-color: #1E90FF;
    color: white;

    .navigation__logo {
      font-weight: bold;
      font-size: 24px;
    }

    .navigation__user {
      font-weight: bold;
    }
  }
}
</style>