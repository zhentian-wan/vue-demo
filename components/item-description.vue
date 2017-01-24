<template>
    <section>
        <h1>Child component {{name }}</h1>
        <div>
            Child button: <button @click="insideInc">Inc from inside {{insideCounter}}</button>
        </div>
    </section>
</template>

<script>
    export default {
        name: 'item-description',
        props: ['counter', 'name'],
        data: function() {
            return {
                insideCounter: this.counter
            }
        },
        methods: {
            insideInc() {
                this.insideCounter += 1;
                this.$emit('total', this.insideCounter);
            }
        }
    }
</script>