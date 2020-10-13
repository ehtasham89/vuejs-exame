<template>
  <div>
      <button @click="saveAction()" class="btn">Submit</button>
  </div>
</template>

<script>
export default {
    props:['qid', 'answer'],
    methods: {
        saveAction() {
            $nuxt.$emit("collect-answer", {id: this.qid, score: this.answer});
            $nuxt.$emit("update-action");
        }
    },
}
</script>
<style scoped>
.btn{
    background: #ccc;
    padding: 10px;
    color: #000
}
</style>