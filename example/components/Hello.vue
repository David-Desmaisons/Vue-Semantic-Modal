<template>
  <div class="hello">

    <vue-semantic-modal v-model="showModal" modal-transition="horizontal flip" :hasImage="true">
      
      <p slot="header">Select a Photo</p>

       <template slot="content">
        <div class="ui medium image">
          <img src="https://semantic-ui.com/images/avatar2/large/rachel.png">
        </div>
        <div class="description">
          <div class="ui header">Default Profile Image</div>
          <p>We've found the following <a href="https://www.gravatar.com" target="_blank">gravatar</a> image associated with your e-mail address.</p>
          <p>Is it okay to use this photo?</p>
        </div>
      </template>

      <template slot="actions" scope="props">
        <div class="ui black deny button" @click="props.close">
          Nope
        </div>
        <div class="ui positive right labeled icon button" @click="props.close">
          Yep, that's me
          <i class="checkmark icon"></i>
        </div>
      </template>

    </vue-semantic-modal>

  <div class="ui positive right button" @click="showModal= !showModal">
    Open Modal
  </div>

  </div>
</template>

<script>
import VueSemanticModal from '../../src/VueSemanticModal'

export default {
  components: {
    VueSemanticModal,
  },
  name: 'hello',
  data () {
    return {
      showModal: false
    }
  },
  methods:{
  }
}
</script>
<style>
@import '~dist/semantic.css';
</style>
