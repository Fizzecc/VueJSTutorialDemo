<template>
  <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot" :class="{ '--exceeded': newTwootCharacterCount > 180 }" >
    <label for="newTwoot"><strong>New Twoot</strong> ({{ newTwootCharacterCount }}/180)</label>
    <textarea id="newTwoot" rows="4" v-model="state.newTwootContent"/>

    <div class="user-profile__create-twoot-type">
      <label for="newTwootType"><strong>Type: </strong></label>
      <select id="newTwootType" v-model="state.selectedTwootType">
        <option :value="option.value" v-for:="(option, index) in state.twootTypes" :key="index">
          {{ option.name }}
        </option>
      </select>
    </div>
    <button>
      Twoot!
    </button>
  </form>
</template>

<script>
import { reactive, computed } from 'vue';

export default {
  name: "CreateTwootPanel",

  setup(props, context) {
    const state = reactive({
      newTwootContent: '',
      selectedTwootType: 'instant',
      twootTypes: [
        { value: 'draft', name: 'Draft' },
        { value: 'instant', name: 'Instant Twoot' }
      ]
    })

    const newTwootCharacterCount = computed(() => state.newTwootContent.length)

    function createNewTwoot() {
      if (state.newTwootContent && state.selectedTwootType !== 'draft') {
        context.emit('add-twoot', state.newTwootContent)
        state.newTwootContent = ''
      }
    }

    return {
      state,
      newTwootCharacterCount,
      createNewTwoot
    }
  }
}
</script>

<style lang="scss" scoped>

.user-profile__create-twoot {
  padding-top: 20px;
  display: flex;
  flex-direction: column;

  &.--exceeded {
    color: red;
    border-color: red;

    button {
      background-color: red;
      border: none;
      color: white;
    }
  }
}
</style>