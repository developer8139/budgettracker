<template>
<div>
    <ul v-bind:key="amount" v-for="amount in amounts">
        <li>{{amount}}</li>
    </ul>
    <h4>Total: {{compute}}</h4>
    <h4>Amount Available: {{amounted}}</h4>
</div>
</template>

<script>
    export default {
        name: "BudgetList",
        data() {
            return {
                final: 0
            }
        },
        props: {
            amounts: Array,
            amounted: String
        },
        
        computed: {
             compute() {
                if(this.amounts.length > 1) {
                    this.final = this.amounts.reduce((prev, curr) => parseInt(prev) + parseInt(curr))
                }

                 return this.final.toFixed(2)
             }
         }
    }
</script>

<style scoped>

</style>
