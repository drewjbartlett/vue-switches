<template>
    <label :class="classObject">
        <span class="vue-switcher__label">
            <span v-if="label" v-text="label"></span>
            <span v-if="!label && enabled" v-text="textEnabled"></span>
            <span v-if="!label && !enabled" v-text="textDisabled"></span>
        </span>

        <input type="checkbox" :disabled="disabled" v-model="enabled">

        <div></div>
    </label>
</template>

<script>

export default {
    name: 'switches',

    props: {
        selected     : false,

        disabled     : false,

        label        : '',

        textEnabled  : {
            default  : 'Enabled'
        },

        textDisabled : {
            default  : 'Disabled'
        },

        color        : {
            default  : 'green'
        },

        size        : {
            default  : 'medium'
        }
    },

    data () {
        return  {
            enabled: !!this.selected
        }
    },

    mounted () {
        this.$emit('input', this.enabled = !!this.selected)
    },

    watch: {
        enabled (val) {
            this.$emit('input', val);
        },

        selected (val) {
            this.enabled = !!val;
        }
    },

    computed: {
        classObject () {

            const { color, size, enabled } = this

            return {
                'vue-switcher' : true,
                ['vue-switcher--unchecked'] : !enabled,
                [`vue-switcher-color--${color}`] : color,
                [`vue-switcher-size--${size}`] : size,
            };

        }
    }
}

</script>


<style lang="scss">
    $color-green: #53b96e;
    $color-blue: #539bb9;
    $color-red: #b95353;
    $color-orange: #b97953;
    $color-shadow: #777;

    // $color-white: #f5f5f5;
    // $color-teal: #00d1B2;
    // $color-blue: #3273DC;
    // $color-red: #00d1B2;
    // $color-yellow: #ffdd57;
    // $color-green: #ff3860;

    // $colors: white, teal, blue, red, yellow, green;

    .vue-switcher {
        position: relative;

        &__label {
            display: block;
            font-size: 10px;
            margin-bottom: 5px;
        }

        input {
            opacity: 0;
            width: 100%;
            height: 100%;
            position: absolute;
            z-index: 1;
        }

        div {
            background: lighten($color-green, 10%);
            height: 10px;
            width: 40px;
            position: relative;
            border-radius: 30px;
            display: -webkit-flex;
            display: -ms-flex;
            display: flex;
            align-items: center;
            justify-content: flex-start;
            cursor: pointer;

            &:after {
                content: '';
                height: 20px;
                width: 20px;
                background-color: $color-green;
                border-radius: 100px;
                display: block;
                box-shadow: 0px 0px 2px $color-shadow;
                transition: all ease .3s;
                position: absolute;
                left: 100%;
                margin-left: -15px;
                cursor: pointer;
            }
        }

        &--unchecked {
            div {
                background-color: lighten($color-green, 20%);
                justify-content: flex-end;

                &:after {
                    left: 15px;
                }
            }

            &.vue-switcher--color {
                &--blue {
                    div {
                        background-color: lighten($color-blue, 20%);
                    }
                }

                &--red {
                    div {
                        background-color: lighten($color-red, 20%);
                    }
                }

                &--orange {
                    div {
                        background-color: lighten($color-orange, 20%);
                    }
                }
            }
        }



        &-color {

            // @each $color in $colors {
            //
            //     &--{$color} {
            //         div,
            //         div:after {
            //             background-color: $color;
            //         }
            //     }
            // }

            &--blue {
                div,
                div:after {
                    background-color: $color-blue;
                }
            }

            &--red {
                div,
                div:after {
                    background-color: $color-red;
                }
            }

            &--orange {
                div,
                div:after {
                    background-color: $color-orange;
                }
            }
        }
    }

</style>
