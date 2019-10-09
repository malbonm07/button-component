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
        <div id="loading" v-else></div>
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
                'button-input--loading' : this.loading,
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
@import '../assets/_spinner';

$color: (
    "boulder": #666,
    "dark-hot-pink": #E6057C,
    "classic-pink": #F06292,
    "classic-rose": #EB3B4D,
    "tango": #F06B18,
    "selective-yellow": #FDDA0A,
    "white": #fff,
    "shadow-medium": blue,
);

/* @function map-get($color) {
    @if($color == "boulder") {
        @return #666;
    }
    @if($color == "dark-hot-pink") {
        @return #F57C00;
    }
    @if($color == "classic-pink") {
        @return #F06292;
    }
    @if($color == "classic-rose") {
        @return blue;
    }
    @if($color == "white") {
        @return #fff;
    }
    @else if($color == "shadow-medium") {
        @return green;
    }
} */

.button-input {
    // @include font-weight(semibold);
    display: flex;
    justify-content: center;
    // transition: background-color .3s background-position .3s border-color .3s;
    transition: .3s;
    border: rem(2px) solid transparent;
    cursor: pointer;
    padding: rem(9px);
    text-decoration: none;
    line-height: 1.13;
    font-size: rem(14px);
    &:disabled {
        cursor: not-allowed;
        &:not(.button-input--loading) {
            border-color: map-get($color, "boulder");
            color: map-get($color, "boulder");
            &:not(.button-input--secondary) {
                background: map-get($color, "boulder");
                color: map-get($color, "white");
            }
        }
    }

    &--primary {
        background-color: map-get($color, "dark-hot-pink");
        color: map-get($color, "white");

        &:hover:enabled,
        &:active:enabled {
            background-color: darken(map-get($color, "dark-hot-pink"), 10%);
            color: map-get($color, "white");
        }

        /* &:focus {
            outline: rem(2px) solid map-get($color, "classic-rose");
            outline-offset: 0;
        } */

        &.button-input--rounded {
            box-shadow: 0 rem(2px) rem(3px) rem(2px) map-get($color, "classic-rose");
        }
    }

    &--secondary {

        border-color: map-get($color, "dark-hot-pink");
        background-color: transparent;
        color: map-get($color, "dark-hot-pink");

        &:hover:enabled,
        &:active:enabled {
            background-color: darken(map-get($color, "dark-hot-pink"), 10%);
            color: map-get($color, "white");
        }

        /* &:focus {
            outline: rem(2px) solid map-get($color, "classic-rose");
            outline-offset: 0;
        } */

        &.button-input--rounded {
            border-color: transparent;
            background-color: transparent;
            color: map-get($color, "dark-hot-color");

            &:hover:enabled,
            &:active:enabled,
            &.button-input--loading {
                border-color: lighten(map-get($color, "dark-hot-pink"), 50%);
                background-color: lighten(map-get($color, "dark-hot-pink"), 50%);
                color: map-get($color, "dark-hot-pink")
            }
        }
    }

    &--gradient {
        background-image: linear-gradient(to right,
        map-get($color, "dark-hot-pink") 0%,
        map-get($color, "tango") 40%, map-get($color, "selective-yellow") 50%,
        map-get($color, "dark-hot-pink") 100%);
        background-size: 200% auto;
        color: map-get($color, "white");

        &:hover:enabled,
        &:active:enabled {
            background-position: right-center;
        }

        /* &:focus {
            outline: rem(2px) solid map-get($color, "classic-rose");
            outline-offset: 0%;
        } */
    }

    &--fluid {
        flex-grow: 0;
        padding: rem(11px);
    }

    &--rounded {
        flex-grow: 0;
        border-radius: 50%;
        padding: rem(11px);
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
