<script setup lang="ts">
import { ref } from 'vue';
import { ArrowDownRightIcon } from 'vue-tabler-icons';
</script>
<template>
    <v-card elevation="10" >
        <v-card-item>
            <v-avatar class="rounded-md bg-lightprimary text-primary mb-5">
                <img src="/images/svgs/icon-paypal.svg" alt="ico" />
            </v-avatar>
            <h6 class="text-subtitle-1 textSecondary">Payments</h6>
            <h4 class="text-h4 mt-1 text-no-wrap">$67,298</h4>
            <div class="pt-2">
                <v-avatar class="bg-lightsuccess text-success" size="20">
                    <ArrowUpLeftIcon size="17" />
                </v-avatar>
                <span class="text-subtitle-1 ml-2 textSecondary">+9%</span>
            </div>
        </v-card-item>
    </v-card>
</template>
