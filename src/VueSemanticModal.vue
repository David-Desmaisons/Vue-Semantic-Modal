<template>
    <div class="ui dimmer modals page modal-component" :class="dimmerClass" :style="{visibility, display, 'animation-duration': animationDuration+'ms'}">
        <div class="ui modal" :class="modalClass" v-on-clickaway="clickAway" :style="{'margin-top': offsetY+'px', visibility, display,'animation-duration': animationDuration+'ms'}">
            <i v-if="showCloseIcon" class="close icon" @click="close"></i>
            
            <div class="header">
                <slot name="header">
                header
                </slot>
            </div>

            <div class="content" :class="{image: hasImage}">
                <slot name="content">
                    <p>Content</p>
                </slot>
            </div>

            <div class="actions">
                <slot name="actions">
                    <div class="ui positive right button" @click="close">
                        OK
                    </div>
                </slot>
            </div>

        </div>
    </div>
</template>

<script>
import { eventAnimationEnd } from './animationHelper'
import { directive as onClickaway } from 'vue-clickaway'

const closed = 'closed'
const opening = 'opening'
const opened = 'opened'
const closing = 'closing'
const changed = 'changed'

function addClass (inicial, name) {
    return name === '' ? inicial : `${inicial} ${name}`
}

function withDirections (animation){
    return [`${animation} up`, `${animation} down`, `${animation} left`, `${animation} right`]
}

const dimmerVariations = ['', 'inverted']
const modalVariations = ['', 'fullscreen', 'basic', 'small', 'large']
const modalTransitions = ['scale', 'drop', 'horizontal flip', 'vertical flip', 'fade', ...withDirections( 'fade'), ...withDirections( 'fly'), ...withDirections( 'swing')]
const props = {
    opened: {
        type: Boolean,
        default: false
    },
    hasImage: {
        type: Boolean,
        default: false
    },
    animationDuration: {
        type: Number,
        default: 500
    },
    showCloseIcon: {
        type: Boolean,
        default: false
    },
    dimmerVariation: {
        type: String,
        default: '',
        validator (value) {
            return dimmerVariations.indexOf(value) !== -1
        }
    },
    modalVariation: {
        type: String,
        default: '',
        validator (value) {
            return modalVariations.indexOf(value) !== -1
        }
    },
    modalTransition: {
        type: String,
        default: 'scale',
        validator (value) {
            return modalTransitions.indexOf(value) !== -1
        }
    }
}

function buildAnimation (name, direction) {
    return `transition animating ${name} ${direction? 'in' : 'out'} visible`
}

function classBuilder (visualState, animation) {
    switch (visualState) {
        case opening:
            return `${buildAnimation(animation,true)} active`

        case opened:
            return 'visible active'

        case closing:
            return buildAnimation(animation,false)

        case closed:
            return ''
    }
}

export default {
    directives: {
        onClickaway: onClickaway,
    },

    props,

    data () {
        return {
            offsetY : 0,
            visualState: closed,
            hidden: true,
            loading: true
        }
    },

    model: {
        prop: 'opened',
        event: changed
    },

    mounted () {
        const modal = this.$el.querySelector('.ui.modal')
        this.modal = modal
        this.offsetY = -modal.clientHeight / 2
        this.loading = false
        this.$el.addEventListener(eventAnimationEnd, this.onAnimationEnded, false)
    },

    beforeDestroy () {
        this.$el.removeEventListener(eventAnimationEnd, this.onAnimationEnded, false)
    },

    methods: {
        close () {
            this.$emit(changed, false)
        },

        open () {
            this.$emit(changed, true)
        },

        clickAway () {
            if (this.visualState!==opened) {
                return
            }
            this.$emit('clickAwayModal')
        },

        onAnimationEnded () {
            this.visualState = this.opened ? opened : closed
        }
    },

    watch: {
        opened (newValue) {
            this.visualState = newValue? opening : closing
        },
        visualState (newValue) {
            this.$emit('displayChanged', newValue)
        }
    },

    computed:{
        dimmerClass () {
            return addClass(classBuilder(this.visualState, 'fade'), this.dimmerVariation)
        },

        modalClass () {
            return addClass(classBuilder(this.visualState,  this.modalTransition), this.modalVariation)
        },

        visibility () {
            return this.loading? 'hidden' : 'visible'
        },

        display () {
            return (this.loading || this.opened) ? 'block' : 'none'
        }
    }
}
</script>

<style>
</style>