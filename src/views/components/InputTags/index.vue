<template>
    <div>
        <a-tag color="#108ee9" v-for="(tag, index) in value" :key="tag + index" closable @close="del(tag)">
            {{ tag }}
        </a-tag>
        <a-input placeholder="input placeholder" @keyup.enter="add" v-model="inputValue"/>
    </div>
</template>
<script>
export default {
    props: ['value'],
    data() {
        return {
            inputValue: ''
        }
    },
    methods: {
        add() {
            console.log(this.inputValue)
            this.$emit('input', this.inputValue, true)
            this.inputValue = ''
        },
        del(tag) {
            this.$emit('input', tag, false)
        }
    }
}
</script>
<style scoped>
    
</style>