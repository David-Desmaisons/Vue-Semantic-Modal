# Vue-Semantic-Modal

Modal component for [semantic-ui](https://semantic-ui.com/) without jQuery

[![GitHub open issues](https://img.shields.io/github/issues/David-Desmaisons/Vue.Semantic.Modal.svg?maxAge=2592000)](https://github.com/David-Desmaisons/Vue.Semantic.Modal/issues)
[![Npm version](https://img.shields.io/npm/v/vue-semantic-modal.svg?maxAge=2592000)](https://www.npmjs.com/package/vue-semantic-modal)
[![vue2](https://img.shields.io/badge/vue-2.x-brightgreen.svg)](https://vuejs.org/)
[![MIT License](https://img.shields.io/github/license/David-Desmaisons/Vue.D3.tree.svg)](https://github.com/David-Desmaisons/Vue.Semantic.Modal/LICENSE)


# Example

![demo](./modal.gif)

# Usage

```html
<modal v-model="showModal">

    <p slot="header">Confirmation needed</p>

    <p slot="content">Do you want to continue?</p>

    <template slot="actions">
        <div class="ui black deny button" @click="showModal=false">
          No
        </div>
        <div class="ui positive right button" @click="confirm">
          Yes
        </div>
    </template>

</modal>
```
```javascript
import modal from 'vue-semantic-modal'

export default {
  components: {
    modal
  },
  data() {
    return {
        showModal: true,
        confirmed: true
    }
  },
  methods () {
    confirm () {
        this.confirmed = true
        this.showModal = false
    }
  }
}
  //...
```

Include in the root component semantic-ui CSS:

```
@import '~dist/semantic.css';
```

# Slot

* `header`

* `content`

* `actions`


# Props

| Name      | Required | Type/Value              | Default     | Description |
| ---       | ---      | ---                     | ---         | ---         |
| opened      | no    | `Boolean`                | false        | triggers the opening/closing. Can be bind with v-model
| hasImage   | no | `Boolean`  | false |  Should be true if the content contains image as per semantic-ui specification |
| animationDuration | no | `Number` |  500       | Opening and closing animation duration in ms |
| showCloseIcon    | no | `Boolean`          | false       | If true close icon of the model is displayed |
| modalVariation   | no | `'fullscreen', 'basic', 'small', 'large' or ''`  | '' |  Additional modal styling [see here](https://semantic-ui.com/modules/modal.html#/definition) |
| dimmerVariation   | no | `'inverted' or ''`  | '' |  Additional dimmer styling [see here](https://semantic-ui.com/modules/modal.html#/examples) |
| modalTransition   | no | `String`  | 'scale'|  name of the modal transition to be applied. [See here](https://semantic-ui.com/modules/transition.html) |

# Events

* `changed`

Sent when the modal state changed with a boolean true if the modal is opened

* `displayChanged`

Sent when the modal visual state changed with a string representing the modal visual state:

`'closed', 'opening', 'opened', 'closing'`

* `clickAwayModal`

Sent when modal is opened and user click outside.


# Installation
- Available through:
``` js
 npm install vue-semantic-modal
```
