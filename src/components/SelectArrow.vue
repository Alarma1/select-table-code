<template>
    <div class="main-box">
        <div>
            <p class="off_placeholder" v-if="selectedOption !== null">Выберите животное</p>
        </div>
        <div class="custom-select-base"
             :class="{['custom-select-open']: isDropdownVisible, ['custom-select-close']: !isDropdownVisible}"
             @click="toggleDropdown">
            <div class="selected-value" :class="{['text-color']:selectedOption !== null}">
                {{ selectedOption ? selectedOption.title : placeholder }}

            </div>
            <div :class="{ rotated: isDropdownVisible }">
                <svg class="arrow-color-base" :class="{['arrow-color']: isDropdownVisible}" width="16" height="16"
                     viewBox="0 0 16 16"
                     fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M3 6L8 11L13 6" stroke-width="2" stroke-linecap="round"
                          stroke-linejoin="round"/>
                </svg>
            </div>
        </div>
        <div :class="{['box-list']: isDropdownVisible}">
            <ul v-if="isDropdownVisible" class="options-list">
                <li class="text-color" v-for="option in options" :key="option.id" @click="selectOption(option)">
                    {{ option.title }}
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            options: {
                type: Array,
                required: true,
            },
            selectedOption: {
                type: Object,
                default: null,
            },
            placeholder: {
                type: String,
                default: 'Выберите животное',
            },
            updateSelectedOption: {
                type: Function,
                required: true,
            },
        },
        data() {
            return {
                isDropdownVisible: false,
            };
        },
        methods: {
            toggleDropdown() {
                this.isDropdownVisible = !this.isDropdownVisible;
            },
            selectOption(option) {
                this.updateSelectedOption(option);
                this.isDropdownVisible = false;
            },
        },
    };
</script>

<style lang="scss" scoped>
    .main-box {
        position: relative;
    }

    .custom-select-base {
        z-index: 2;
        padding: 10px;
        display: flex;
        justify-content: space-between;
        position: relative;
        background-color: white;
        border-radius: 9px;
        color: #29277d;
        cursor: pointer;
        user-select: none;
    }

    .custom-select-open {
        position: relative;
    }

    .custom-select-open:before {
        content: "";
        position: absolute;
        inset: 0;
        border-radius: 10px 10px 0px 0px;
        padding: 1px;
        background: linear-gradient(0deg, #6ed8ff, #ff8cde);
        -webkit-mask: linear-gradient(#fff 0 0) content-box,
        linear-gradient(#fff 0 0);
        -webkit-mask-composite: xor;
        mask-composite: exclude;
        pointer-events: none;
    }

    .custom-select-close {
        border: 1px solid grey;
    }

    .selected-value {
        color: rgba(41, 39, 125, 0.40);
        transition: background-color 0.3s;
    }

    .text-color {
        color: #29277d;
    }

    .box-list {
        margin-top: -1px;
        position: relative;
    }

    .options-list {
        list-style: none;
        padding: 0;
        margin: 0;
        border-radius: 0 0 10px 10px;
        border-top: none;
        z-index: 1;
        background-color: #fff;
    }

    .options-list li {
        padding: 10px;
        cursor: pointer;
        transition: background-color 0.3s;
    }

    .box-list:before {
        content: "";
        position: absolute;
        inset: 0;
        border-top: none;
        border-radius: 0px 0px 10px 10px;
        padding: 1px;
        background: linear-gradient(0deg, #6ed8ff, #ff8cde);
        -webkit-mask: linear-gradient(#fff 0 0) content-box,
        linear-gradient(#fff 0 0);
        -webkit-mask-composite: xor;
        mask-composite: exclude;
        pointer-events: none;
    }

    .options-list li:hover {
        background-color: #DADEFE;
    }

    .off_placeholder {
        color: rgba(41, 39, 125, 0.40);
        z-index: 3;
        position: absolute;
        top: -10px;
        background: white;
        margin: 0;
    }

    .rotated {
        transform: rotate(180deg);
    }

    .arrow-color-base {
        stroke: #BBC3FF;
    }

    .arrow-color {
        stroke: #5F88F4;
    }
</style>
