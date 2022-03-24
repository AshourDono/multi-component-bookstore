<template>
    <div class="bg-dark d-flex flex-row justify-content-between p-3 m-2">
        <h3>
          <a href="#" class="text-white text-decoration-none" @click="changeVisible">Books</a>
        </h3>
        <button class="btn btn-success" @click="changeVisible">Wishlist ({{cart}})</button>
      </div>
</template>
<script>
export default {
    methods:{
        changeVisible() {
            this.$emit('change-visible');
          },
    },
    props:{
        cart:{
            type:Number
        }
    }
}
</script>
<style scoped>

</style>