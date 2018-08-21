<template>
    <label :class="classObject">
        <span class="vue-switcher__label" v-if="shouldShowLabel && ! inlineLabel">
            <span v-if="label" v-text="label"></span>
            <span v-if="!label && value" v-text="textEnabled"></span>
            <span v-if="!label && !value" v-text="textDisabled"></span>
        </span>

        <input type="checkbox" :disabled="disabled" @change="trigger" :checked="value">

        <div><span class="vue-switcher__inlineLabel" v-if="shouldShowLabel && inlineLabel">
            <span v-if="label" v-text="label" class="vue_switcher__container"><span v-text="label"></span></span>
            <span v-if="!label && value" v-visible="value" class="vue_switcher__container"><span  v-text="textEnabled"></span></span>
            <span v-if="!label && !value" v-visible="!value" class="vue_switcher__container"><span v-text="textDisabled"></span></span>
            <span class="vue_switcher__width-placeholder" v-text="longestText"></span>
        </span></div>
    </label>
</template>

<script>

  export default {
    name: 'switches',

    props: {
      typeBold: {
        default: false
      },

      value: {
        default: false
      },

      disabled: {
        default: false
      },

      label: {
        default: ''
      },

      inlineLabel: {
        default: false
      },

      textEnabled: {
        default: ''
      },

      textDisabled: {
        default: ''
      },

      color: {
        default: 'default'
      },

      theme: {
        default: 'default'
      },

      emitOnMount: {
        default: true
      }
    },

    mounted () {
      if(this.emitOnMount) {
        this.$emit('input', this.value)
      }
    },

    methods: {
      trigger (e) {
        this.$emit('input', e.target.checked)
      }
    },

    computed: {
      longestText () {
        return this.label || this.textEnabled.length > this.textDisabled.length ? this.textEnabled : this.textDisabled
      },
      classObject () {

        const { color, value, theme, typeBold, disabled } = this;

        return {
          'vue-switcher' : true,
          ['vue-switcher--unchecked'] : !value,
          ['vue-switcher--disabled'] : disabled,
          ['vue-switcher--bold']: typeBold,
          ['vue-switcher--bold--unchecked']: typeBold && !value,
          [`vue-switcher-theme--${theme}`] : color,
          [`vue-switcher-color--${color}`] : color,
        };

      },

      shouldShowLabel () {
        return this.label !== '' || this.textEnabled !== '' || this.textDisabled !== '';
      }
    },
    directives: {
      visible: {
        update: (el, binding) => {
          var value = binding.value;

          if (!!value) {
            el.style.visibility = 'visible';
          } else {
            el.style.visibility = 'hidden';
          }
        }
      }
    }
  }

</script>

<style src="./../dist/switches.css"></style>
