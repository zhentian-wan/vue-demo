<template>
    <div>
        Edit component: <input type="text" v-model="editValue"/>
    </div>
</template>
<script>
    export default{
        name: 'edit-component',
        data(){
            return{
                editValue: this.name
            }
        },
        props: ['name']
    }
</script>
