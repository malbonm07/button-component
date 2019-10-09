<template>
    <component
    :is="tag"
    :class="getClasses"
    class="button-input"
    :disabled="loading || disabled"
    @click="onClick"
    >
    <span>
        <slot v-if="!rounded"></slot>
        <div id="btnSpinner" v-else></div>
    </span>
    </component>
</template>

<script>
const AVAILABLE_CATEGORIES = [ 'primary', 'secondary', 'gradient']

export default {
    name: "ButtonInput",

    components: {},

    props: {
        fluid: {
            type: Boolean,
            default: false
        },
        tag: {
            type: String,
            default: "button"
        },
        rounded: {
            type: Boolean,
            default: false
        },
        loading: {
            type: Boolean,
            default: false
        },
        disabled: {
            type: Boolean,
            default: false
        },
        category: {
            type: String,
            default: "primary",
            validator: function (value) {
                return AVAILABLE_CATEGORIES.includes(value);
            }
        }
    },

    computed: {
        getClasses() {

            return {
                'button-input--rounded': this.rounded,
                [`button-input--${this.category}`] : this.category,
                'button-input--fluid' : this.fluid,
                'button-input--loading' : this.loading
            }
        }
    },

    methods: {
        onClick() {
            this.$emit('click');
        }
    }
}
</script>

<style lang="scss">
@import '../assets/_rem';

@function get-color($color) {
    @if($color == "boulder") {
        @return #666;
    }
    @if($color == "dark-hot-pink") {
        @return #F57C00;
    }
    @if($color == "classic-pink") {
        @return #F06292;
    }
    @if($color == "white") {
        @return #fff;
    }
    @if($color == "shadow-medium") {
        @return blue;
    }
}

.button-input {
    // @include font-weight(semibold);
    display: flex;
    justify-content: center;
    // transition: background-color .3s background-position .3s border-color .3s;
    transition: .3s;
    border: rem(4px) solid transparent;
    cursor: pointer;
    padding: rem(9px);
    text-decoration: none;
    line-height: 1.13;
    font-size: rem(14px);
    :disabled {
        cursor: not-allowed;
        &:not(.button-input--loading) {
            border-color: get-color("boulder");
            color: get-color("boulder");
            &:not(.button-input--secondary):not(.button-input--no-background) {
                background: get-color("boulder");
                color: get-color("white");
            }
        }
    }

    &--primary {
        background-color: get-color("dark-hot-pink");
        color: get-color("white");

        &:hover:enabled,
        &:active:enabled {
            background-color: darken(get-color("dark-hot-pink"), 10%);
            color: get-color("white");
        }

        &:focus {
            outline: rem(2px) solid get-color("classic-rose");
            outline-offset: 0;
        }

        &.button-input--rounded {
            box-shadow: 0 rem(2px) rem(3px) rem(2px) get-color("shadow-medium");
        }
    }

    &--secundary {

        border-color: get-color("dark-hot-pink");
        background-color: transparent;
        color: get-color("dark-hot-pink");

        &:hover:enabled,
        &:active:enabled {
            background-color: darken(get-color("dark-hot-pink"), 10%);
            color: get-color("white");
        }

        &:focus {
            outline: rem(2px) solid get-color("classic-rose");
            outline-offset: 0;
        }

        &.button-input--rounded {
            border-color: transparent;
            background-color: transparent;
            color: get-color("dark-hot-color");

            &:hover:enabled,
            &:active:enabled,
            &.button-input--loading {
                border-color: lighten(get-color("dark-hot-pink"), 50%);
                background-color: lighten(get-color("dark-hot-pink"), 50%);
                color: get-color("dark-hot-pink")
            }
        }
    }

    &--gradient {
        background-image: linear-gradient(to right,
        get-color("dark-hot-pink") 0%,
        get-color("tango") 40%, get-color("selective-yellow") 50%,
        get-color("dark-hot-pink") 100%);
        background-size: 200% auto;
        color: get-color("white");

        &:hover:enabled,
        &:active:enabled {
            background-position: right-center;
        }

        &:focus {
            outline: rem(2px) solid get-color("classic-rose");
            outline-offset: 0%;
        }
    }

    &--fluid {
        flex-grow: 0;
        padding: rem(11px);
    }

    &--rounded {
        flex-grow: 0;
        border-radius: 100%;
        padding: rem(50px);
    }

    span {
        display: grid;
        align-items: center;
        grid-auto-flow: columns;
        grid-gap: rem(0px);
    }

    button {
        outline: inherit;
        border: 0;
        background: none;
    }
}
</style>
