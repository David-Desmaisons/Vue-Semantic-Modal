<template>
  <div class="hello">


    <div class="ui container">

      <form class="ui form">
      <h4 class="ui dividing header">Modal Props</h4>


      <div class="three fields">
        <div class="field">
          <label>Modal Varition</label>
          <select v-model="modalVariation" class="ui fluid dropdown">
              <option v-for="option in modalVariations" :value="option">
                  {{ option }}
              </option>
          </select>
        </div>

        <div class="field">
          <label>Dimmer Varition</label>
          <select v-model="dimmerVariation" class="ui fluid dropdown">
            <option v-for="option in dimmerVariations" :value="option">
                  {{ option }}
              </option>
          </select>
        </div>

        <div class="field">
          <label>Modal Transition</label>
          <select v-model="modalTransition" class="ui fluid dropdown">
              <option v-for="option in modalTransitions" :value="option">
                  {{ option }}
              </option>
          </select>
        </div>
        
      </div>

      <div class="field">
        <div class="three fields">
          <div class="four wide field">
              <div class="ui toggle checkbox">
                <input v-model="closeOnClickAway" type="checkbox">
                <label>Close On ClickAway</label>
              </div>
          </div>

          <div class="four wide field">
            <div class="ui toggle checkbox">
                <input v-model="showCloseIcon" type="checkbox">
                <label>Show Close Icon</label>
              </div>
          </div>

          <div class="eight wide field">
            <div class="ui slider range">
                <input v-model.number="animationDuration" type="range" min="0" max="1000">
                <label>Animation Duration ({{animationDuration}} ms)</label>
              </div>
          </div>
        </div>
      </div>

       <div class="ui positive right button" @click="showModal= !showModal">
        Open Modal
      </div>

      <h4 class="ui dividing header"></h4>
    </form>
  </div>

    <vue-semantic-modal v-model="showModal" :modal-transition="modalTransition" :modal-variation="modalVariation" :dimmer-variation="dimmerVariation" :animation-duration="animationDuration" :hasImage="true" :close-on-click-away="closeOnClickAway" :show-close-icon="showCloseIcon" >
      
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

  </div>
</template>

<script>
import VueSemanticModal from '../../src/VueSemanticModal'

function withDirections (animation){
    return [`${animation} up`, `${animation} down`, `${animation} left`, `${animation} right`]
}

export default {
  components: {
    VueSemanticModal,
  },
  name: 'hello',
  data () {
    return {
      showCloseIcon: false,
      closeOnClickAway: true,
      showModal: false,
      animationDuration: 500,
      dimmerVariation: '',
      modalVariation: '',
      modalTransition: 'scale',
      dimmerVariations : ['', 'blurring', 'inverted'],
      modalVariations : ['', 'fullscreen', 'basic', 'small', 'large'],
      modalTransitions : ['scale', 'drop', 'horizontal flip', 'vertical flip', 'fade', ...withDirections( 'fade'), ...withDirections( 'fly'), ...withDirections( 'swing')]
    }
  },
  methods:{
  }
}
</script>
<style>
@import '~dist/semantic.css';

.ui.slider.range>input[type="range"] {
  width: 60%
}

input[type="range"] {
  width: 100%;
  -webkit-appearance: none;
  border: 1px solid #ddd;
  padding: 0;
  height: 0;
  margin-top: 1rem;
  margin-bottom: 1rem;
}

input[type="range"]:focus {
  border-color: #ccc;
  outline: none !important;
}

input[type="range"]::-moz-range-track {
  background: none;
  border: 0;
}

input[type="range"]::-moz-focus-outer {
  border: 0;
}

input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  //border: 1px solid #ddd;
  height: 1.5rem;
  width: 1.5rem;
  background: #fff;
  background: #fff linear-gradient(transparent, rgba(0, 0, 0, 0.05));
  background: #fff -webkit-linear-gradient(transparent, rgba(0, 0, 0, 0.05));
  background: #fff -o-linear-gradient(transparent, rgba(0, 0, 0, 0.05));
  background: #fff -moz-linear-gradient(transparent, rgba(0, 0, 0, 0.05));
  border-radius: 100%;
  box-shadow: 0 1px 2px 0 rgba(34, 36, 38, .15), 0 0 0 1px rgba(34, 36, 38, .15) inset;
}

input[type="range"]::-moz-range-thumb {
  //border: 1px solid #ddd;
  height: 1.5rem;
  width: 1.5rem;
  background: #fff;
  background: #fff linear-gradient(transparent, rgba(0, 0, 0, 0.05));
  background: #fff -webkit-linear-gradient(transparent, rgba(0, 0, 0, 0.05));
  background: #fff -o-linear-gradient(transparent, rgba(0, 0, 0, 0.05));
  background: #fff -moz-linear-gradient(transparent, rgba(0, 0, 0, 0.05));
  border-radius: 100%;
  box-shadow: 0 1px 2px 0 rgba(34, 36, 38, .15), 0 0 0 1px rgba(34, 36, 38, .15) inset;
}
</style>
