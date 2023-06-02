<script setup lang="ts">
import { ref, onMounted, computed } from 'vue';
import { useEcomStore } from '@/stores/apps/eCommerce';

const panel = ref([0, 1, 2, 3, 4]);
const priceSort = [
    {
        label: 'Below $10',
        price: '10'
    },
    {
        label: '$10 - $50',
        price: '10-50'
    },
    {
        label: '$50 - $100',
        price: '50-100'
    },
    {
        label: '$100 - $150',
        price: '100-150'
    },
    {
        label: '$150 - $200',
        price: '150-200'
    },
    {
        label: 'Over $200',
        price: '200'
    }
];

const store = useEcomStore();

const selectedGender = ref('');
store.SelectGender(selectedGender);

const selectedCategory = ref('all');
store.SelectCategory(selectedCategory);

const selectPrice = ref(0);
const selectRating = ref(1);
const setColor = ref(1);
function selectColor(e: any) {
    setColor.value = e;
}

onMounted(() => {
    store.fetchProducts();
});

const getProducts = computed(() => {
    return store.products;
});
const getUniqueData = (data: any, attr: any) => {
    let newVal = data.map((curElem: any) => {
        return curElem[attr];
    });
    if (attr === 'colors') {
        newVal = newVal.flat();
    }

    return (newVal = [...Array.from(new Set(newVal))]);
};

const filterbyColors: any = computed(() => {
    return getUniqueData(getProducts.value, 'colors');
});
</script>
<template>
    <v-sheet class="pa-4 pt-1">
        <v-expansion-panels v-model="panel" multiple>
            <v-expansion-panel elevation="0">
                <v-expansion-panel-title class="font-weight-medium custom-accordion"> Gender </v-expansion-panel-title>
                <v-expansion-panel-text class="acco-body">
                    <v-row no-gutters>
                        <v-col cols="12">
                            <v-checkbox label="Male" v-model="selectedGender" color="primary" value="male" hide-details> </v-checkbox>
                        </v-col>
                        <v-col cols="12">
                            <v-checkbox label="Female" v-model="selectedGender" color="secondary" value="female" hide-details></v-checkbox>
                        </v-col>
                        <v-col cols="12">
                            <v-checkbox label="Kids" v-model="selectedGender" color="error" value="kids" hide-details></v-checkbox>
                        </v-col>
                    </v-row>
                </v-expansion-panel-text>
            </v-expansion-panel>
            <v-divider />
            <v-expansion-panel elevation="0">
                <v-expansion-panel-title class="font-weight-medium custom-accordion"> Categories </v-expansion-panel-title>
                <v-expansion-panel-text class="acco-body">
                    <v-row no-gutters>
                        <v-col cols="12">
                            <v-checkbox label="All" v-model="selectedCategory" color="primary" value="all" hide-details> </v-checkbox>
                        </v-col>
                        <v-col cols="12">
                            <v-checkbox
                                label="Kitchen"
                                v-model="selectedCategory"
                                color="primary"
                                value="kitchen"
                                hide-details
                            ></v-checkbox>
                        </v-col>
                        <v-col cols="12">
                            <v-checkbox
                                label="Electronics"
                                v-model="selectedCategory"
                                color="primary"
                                value="electronics"
                                hide-details
                            ></v-checkbox>
                        </v-col>
                        <v-col cols="12">
                            <v-checkbox label="Books" v-model="selectedCategory" color="primary" value="books" hide-details></v-checkbox>
                        </v-col>
                        <v-col cols="12">
                            <v-checkbox
                                label="Fashion"
                                v-model="selectedCategory"
                                color="primary"
                                value="fashion"
                                hide-details
                            ></v-checkbox>
                        </v-col>
                        <v-col cols="12">
                            <v-checkbox label="Toys" v-model="selectedCategory" color="primary" value="toys" hide-details></v-checkbox>
                        </v-col>
                    </v-row>
                </v-expansion-panel-text>
            </v-expansion-panel>
            <v-divider />
            <v-expansion-panel elevation="0">
                <v-expansion-panel-title class="font-weight-medium custom-accordion"> Colors </v-expansion-panel-title>
                <v-expansion-panel-text class="acco-body">
                    <div class="d-flex gap-2 flex-wrap v-col-11 px-0">
                        <template v-for="(catcolor, i) in filterbyColors" :key="i" v-if="filterbyColors.length > 0">
                            <v-avatar
                                class="cursor-pointer"
                                :color="catcolor"
                                variant="flat"
                                size="small"
                                @click="store.sortByColor(catcolor)"
                            >
                                <template v-if="store.color === catcolor">
                                    <CheckIcon size="13" />
                                </template>
                            </v-avatar>
                        </template>
                    </div>
                </v-expansion-panel-text>
            </v-expansion-panel>
            <v-divider />
            <v-expansion-panel elevation="0">
                <v-expansion-panel-title class="font-weight-medium custom-accordion"> Price </v-expansion-panel-title>
                <v-expansion-panel-text class="acco-body">
                    <v-radio-group v-model="store.price" class="custom-radio-box">
                        <v-radio
                            v-for="pricing in priceSort"
                            :key="pricing.label"
                            :label="pricing.label"
                            v-model="store.price"
                            color="primary"
                            :value="pricing.price"
                            hide-details
                        >
                        </v-radio>
                    </v-radio-group>
                </v-expansion-panel-text>
            </v-expansion-panel>
            <v-divider />
            <v-expansion-panel elevation="0">
                <v-expansion-panel-title class="font-weight-medium custom-accordion"> Rating </v-expansion-panel-title>
                <v-expansion-panel-text class="acco-body">
                    <v-rating hover color="warning" v-model="selectRating" class="ma-2" density="compact"></v-rating>
                </v-expansion-panel-text>
            </v-expansion-panel>
        </v-expansion-panels>
        <v-btn color="primary" block class="mt-5" flat>Reset Filters</v-btn>
    </v-sheet>
</template>
<style lang="scss">
.custom-accordion {
    padding: 18px 2px;

    min-height: 30px !important;
    .v-expansion-panel-title__overlay {
        background-color: transparent;
    }
}
.acco-body {
    .v-expansion-panel-text__wrapper {
        padding: 5px 0;
    }
}
.custom-radio-box {
    .v-selection-control-group {
        // flex-direction: row;
        flex-wrap: wrap;
    }
}

// @media (max-width: 1279px) {
//     .lgScroll {
//         height: calc(100vh - 95px) !important;
//     }
// }
</style>
