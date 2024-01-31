<template>
    <div>Mon composant de test {{ msg }}</div>
</template>
<script>
    export default {
        name: "TestComponent", 
        props: {
            msg: String 
        }
    }
</script>