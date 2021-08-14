<template>
<div>
    <ul v-bind:key="amount" v-for="amount in amounts">
        <li>${{amount.amount}} <button v-on:click="deletesAmount(amount.id)">Delete</button></li>
    </ul>
    <h4>Total: {{compute}}</h4>
    <h4>Amount Available: {{amounted}}</h4>
    <h4>Amount Left: {{subtract}}</h4>
</div>
</template>

<script>
    export default {
        name: "BudgetList",
        data() {
            return {
                final: 0,
                amounted: 0,
                left: 0
            }
        },
        props: {
            amounts: Array,
        },
        created() {
            let store = window.localStorage;
            this.amounted = store.getItem('amount')
        },
        computed: {
             compute() {
                if(this.amounts.length > 1) {
                    this.final = this.amounts.reduce((prev, curr) => parseInt(prev.amount) + parseInt(curr.amount))
                }

                 return this.final.toFixed(2)
             },

             subtract() {
                 this.left = this.amounted - this.final;
                 return this.left.toFixed(2)
             }
         },
         methods: {
             deletesAmount(id) {
                 this.$emit('deleted', id)
             }
         }
    }
</script>

<style scoped>
    li {
        list-style: none;
        border: 1px solid red;
        padding: 15px;
        border-radius: 5px;
    }
</style>
