<template>
<div>
    <h1>BudgetAmounts</h1>
    <form @submit.prevent="getAmounts">
        <input type="text" placeholder="Enter an amount..." v-model="amounted"/>
        <button>Enter Amount</button>
    </form>
    <BudgetList v-bind:amounts="this.amounts"/>
</div>
</template>

<script>
    import BudgetList from './BudgetList.vue';


    export default {
        name: "BudgetAmounts",
        components: {
            BudgetList
        },
        data() {
            return {
                amounted: "",
                amounts: [],
                final: 0
            }
        },
        methods: {
            getAmounts() {
                this.amounts = [...this.amounts, this.amounted];
                this.amounted = ""
            }
        }
    }

</script>

<style scoped>

</style>
