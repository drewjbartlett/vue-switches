# Vue Switches
A Vue.js component for simple switches with theme support for [bulma](http://bulma.io), [bootstrap](http://getbootstrap.com/) and custom themes. See a live demo [here](http://drewjbartlett.com/demos/vue-switches/).

<img src="http://cagefreeproduce.com/images/vue-switches.png" />
<br />
<br />
<img src="http://i1123.photobucket.com/albums/l554/DoctorOz_Oz/swi.png" />

## Installation

```bash
    npm install vue-switches --save
```

## Basic Usage

```javascript
import Switches from 'vue-switches';

new Vue({

    components: {
        Switches
    },

    data () {
        return {
            enabled: false
        }
    }
};
```

```html

<switches v-model="enabled" :selected="enabled"></switches>

```

## Props

`label` - A static label to always display whether on or off. <br /> 
`text-enabled` - The text that displays when enabled. <br />
`text-disabled` - The text that displays when disabled. <br />
`theme` - Which theme to use. <br />
`color` - Which color to use. <br />
`type-bold` - Bigger style. <br />


## Theme Support
Out of the box `vue-switches` supports a default, [bulma](http://bulma.io), [bootstrap](http://getbootstrap.com/) themes. To use them you can do as follows:

Providing no `theme` or `color` props would render a switch of default theme and color.

```html

 <switches v-model="enabled" :selected="enabled"></switches>

```

Available colors for `default` are `default`, `red`, `blue`, `green`, and `yellow`, and `orange.


```html

    <switches v-model="enabled" :selected="enabled" theme="bulma" color="default"></switches>

```

Available colors for Bulma are `default`, `primary`, `red`, `blue`, `green`, and `yellow`.

In addition support for bootstrap can be used as follows:

```html

<switches v-model="enabled" :selected="enabled" theme="bootstrap" color="danger"></switches>

```

Available colors for Bulma are `default`, `primary`, `success`, `info`, `warning`, and `danger`.

A demo of all themes can be seen [here](http://drewjbartlett.com/demos/vue-switches/).

## Making Your Own Themes
Vue Switcher has a base class of  `.vue-switcher`. For an unchecked switch a class of `.vue-switcher--unchecked` is applied. Lastly, for the `theme` and `color` props a class is also applied. So for a `bulma` theme of color `primary` the classes `.vue-switcher-theme--bulma` and `.vue-switcher-color--primary`.

This:
```html

<switches v-model="enabled" :selected="enabled" type-bold="false" theme="custom" color="blue"></switches>

```

Would render the classes `.vue-switcher-theme--custom` and `.vue-switcher-color--blue`. Sass for this theme could look like:

```css
.vue-switcher-theme--custom {
    &.vue-switcher-color--blue {
        div {
            background-color: lighten(blue, 10%);

            &:after {
                // for the circle on the switch
                background-color: darken(blue, 5%);
            }
        }

        &.vue-switcher--unchecked {
            div {
                background-color: lighten(blue, 30%);

                &:after {
                    background-color: lighten(blue, 10%);
                }
            }
        }
    }
}
```

For better understanding, below is how the class object is rendered.
```javascript
classObject () {

    const { color, enabled, theme } = this;

    return {
        'vue-switcher' : true,
        ['vue-switcher--unchecked'] : !enabled,
        ['vue-switcher--disabled'] : disabled,
        [`vue-switcher-theme--${theme}`] : color,
        [`vue-switcher-color--${color}`] : color,
    };

}
```
