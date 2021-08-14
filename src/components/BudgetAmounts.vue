<template>
<div class="container">
    <h1>BudgetAmounts</h1>
    <form @submit.prevent="getAmounts">
        <input type="text" placeholder="Enter an amount..." v-model="amounted"/>
        <button>Enter Amount</button>
    </form>
    <BudgetList v-on:deleted="deleteBtn($event)" v-bind:amounts="this.amounts"/>
</div>
</template>

<script>
    import BudgetList from './BudgetList.vue';
    import {v4 as uuid} from 'uuid';


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
                if(this.amounted === "" || this.amounted.includes(',')) {
                    return
                }

                let budgetAmount = {
                    amount: this.amounted,
                    id: uuid()
                }


                this.amounts = [...this.amounts, budgetAmount];
                this.amounted = ""
            },

             deleteBtn(id) {
                this.amounts = this.amounts.filter(amount => amount.id !== id)
            }
        }
    }

</script>

<style scoped>
    .container {
        display: flex;
        flex-direction: column;
        border: 1px solid lightcyan;
        border-radius: 10px;
        padding: 20px;
    }
</style>
