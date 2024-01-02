<template>
    <div id="app">
        <div class="dimensions">
            <SelectArrow
                    :options="options"
                    :selectedOption="selectedOption"
                    :updateSelectedOption="updateSelectedOption"
            ></SelectArrow>
        </div>
        <TableComponent :titles="titles" :tables="tables"/>
    </div>
</template>

<script>
    import SelectArrow from "@/components/SelectArrow";
    import TableComponent from "@/components/TableComponent";

    export default {
        data() {
            return {
                options: [
                    {id: 1, title: 'Слон'},
                    {id: 2, title: 'Бегемот'},
                    {id: 3, title: 'Зебра'},
                    {id: 4, title: 'Жираф'},
                    {id: 5, title: 'Лев'},
                ],
                selectedOption: null,
                titles: [
                    {id: 1, title: 'Номер', key: 'number'},
                    {id: 2, title: 'Девелопер', key: 'developer'},
                    {id: 3, title: 'Срок', key: 'deadline'},
                    {id: 4, title: 'Тип', key: 'type'},
                    {id: 5, title: 'Этаж', key: 'floor'},
                    {id: 6, title: 'Площадь', key: 'square'}
                ],
                tables: [
                    {
                        id: 1,
                        number: 421,
                        developer: 'PRINZIP',
                        deadline: '2005-08-09T18:31:42',
                        type: 'Студия',
                        floor: 2,
                        square: 100.3
                    },
                    {
                        id: 2,
                        number: 73,
                        developer: 'Брусника',
                        deadline: '2005-08-09T18:31:42',
                        type: '2-к',
                        floor: 2,
                        square: 10.3
                    },
                    {
                        id: 3,
                        number: 122,
                        developer: 'TEN',
                        deadline: '2005-08-09T18:31:42',
                        type: '3-к',
                        floor: 2,
                        square: 103
                    },
                    {
                        id: 4,
                        number: 1,
                        developer: 'PRINZIP',
                        deadline: '2023-08-09T18:31:42',
                        type: 'Студия',
                        floor: 2,
                        square: 100.3
                    },
                    {
                        id: 5,
                        number: 72,
                        developer: 'Брусника',
                        deadline: '2005-08-09T18:31:42',
                        type: '2-к',
                        floor: 2,
                        square: 10.3
                    },
                    {
                        id: 6,
                        number: 23,
                        developer: 'TEN',
                        deadline: '2005-08-09T18:31:42',
                        type: '3-к',
                        floor: 2,
                        square: 103
                    },
                    {
                        id: 7,
                        number: 5,
                        developer: 'PRINZIP',
                        deadline: '2005-08-09T18:31:42',
                        type: 'Студия',
                        floor: 2,
                        square: 100.3
                    },
                    {
                        id: 8,
                        number: 2,
                        developer: 'Брусника',
                        deadline: '2005-08-09T18:31:42',
                        type: '2-к',
                        floor: 2,
                        square: 10.3
                    },
                    {
                        id: 9,
                        number: 97,
                        developer: 'TEN',
                        deadline: '2005-08-09T18:31:42',
                        type: '3-к',
                        floor: 2,
                        square: 103
                    },
                    {
                        id: 10,
                        number: 34,
                        developer: 'PRINZIP',
                        deadline: '2005-08-09T18:31:42',
                        type: 'Студия',
                        floor: 2,
                        square: 100.3
                    },
                    {
                        id: 11,
                        number: 1,
                        developer: 'Брусника',
                        deadline: '2005-08-09T18:31:42',
                        type: '2-к',
                        floor: 2,
                        square: 10.3
                    },
                    {
                        id: 12,
                        number: 88,
                        developer: 'TEN',
                        deadline: '2005-08-09T18:31:42',
                        type: '3-к',
                        floor: 2,
                        square: 103
                    }
                ],
            };
        },
        components: {
            TableComponent,
            SelectArrow,
        },
        mounted() {
            const newKey = 'dynamicSvg';
            const newValue = false;
            this.titles = this.titles.map(obj => ({...obj, [newKey]: newValue,}));

        },
        methods: {
            updateSelectedOption(option) {
                this.selectedOption = option;
            },
        },
    };
</script>
<style lang="scss" scoped>
    .dimensions {
        padding: 10px;
        height: 240px;
        width: 250px;
        margin-top: 20px;
    }
</style>
