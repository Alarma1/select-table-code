<template>
    <div>
        <table border="2px" cellspacing="1px" class="main_table">
            <thead>
            <tr class="table_scroll">
                <th class="head-table" v-for="title in titles" :key="title.id"
                    @click="sortFunc(title, title.key)">
                    {{ title.title }}
                    <svg class="svg-arrow" :class="{['svg-arrow--color']:title.dynamicSvg}"
                         xmlns="http://www.w3.org/2000/svg"
                         width="8"
                         height="8"
                         viewBox="0 0 6 5"
                         fill="none">
                        <path opacity="0.3"
                              d="M3.43301 4.25L5.16506 1.25C5.35751 0.916667 5.11695 0.5 4.73205 0.5H1.26795C0.883049 0.5 0.642486 0.916666 0.834936 1.25L2.56699 4.25C2.75944 4.58333 3.24056 4.58333 3.43301 4.25Z"
                              stroke-linejoin="round"/>
                    </svg>
                </th>

            </tr>
            </thead>
            <tbody>
            <tr v-for="table in tablesData" :key="table.id">
                <td class="table_elem">{{ table.number }}</td>
                <td class="table_elem">{{ table.developer }}</td>
                <td class="table_elem">{{ changeData(table.deadline) }}</td>
                <td class="table_elem">{{ table.type }}</td>
                <td class="table_elem">{{ table.floor }}</td>
                <td class="table_elem">{{ table.square }}</td>
            </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        props: {
            tables: {
                type: Array,
                required: true,
            },
            titles: {
                type: Array,
                required: true,
            },
        },
        data() {
            return {
                tablesData: null,
                dynamicSort: 1,
                dynamicSvg: {}
            }
        },
        mounted() {
            this.tablesData = this.tables
        },
        methods: {
            sortFunc(title, key) {
                this.onSvg(key)
                this.dynamicSort *= -1
                if (key === 'number' || key === 'floor' || key === 'square' || key === 'deadline') {
                    this.tablesData = this.tablesData.sort((a, b) => {
                        return this.dynamicSort * (parseFloat(a[key]) - parseFloat(b[key]))
                    })
                }
                if (key === 'developer' || key === 'type') {
                    this.tablesData = this.tablesData.sort((a, b) => {
                        const comparison = a[key].localeCompare(b[key]);
                        return this.dynamicSort * comparison
                    });
                }
            },
            changeData(elem) {
                const deadLine = new Date(elem)
                return deadLine.toISOString();
            },
            onSvg(clickedTitle) {
                this.titles.forEach(title => {
                    title.dynamicSvg = false;
                    if (title.key === clickedTitle) {
                        title.dynamicSvg = true;
                    }
                })
            }
        }
    };
</script>

<style lang="scss" scoped>
    .main_table {
        height: 600px;
    }

    .table_scroll {
        position: sticky;
        top: 0;
    }

    .head-table {
        background-color: lightgray;
        width: 300px;
        height: 50px;
    }

    .head-table:hover {
        cursor: pointer;
    }

    .svg-arrow {
        stroke: red;
    }

    .svg_arrow_color {
        stroke: #29277d;
    }

    .table_elem {
        text-align: center;
    }
</style>
