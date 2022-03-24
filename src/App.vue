<template>
  <NavbarComponent @change-visible="changeVisible" :cart="cart"/>
  <CardComponent @add-to-wishlist="addToWishlist" :isVisible="isVisible" :wishlist="wishlist"/>
  <TableComponent @remove-from-wishlist="removeFromWishlist" :isVisible="isVisible" :wishlist="wishlist"/>
</template>

<script>
import NavbarComponent from "./components/NavbarComponent.vue";
import CardComponent from './components/CardComponent.vue'
import TableComponent from './components/TableComponent.vue'

export default {
  name: 'App',
  data(){
    return{
      isVisible: false,
      cart: 0,
      wishlist: [],
    }
  },
  methods:{
    changeVisible() {
        this.isVisible = !this.isVisible;
    },
    addToWishlist(book){
      this.wishlist.push({ book: book });
      this.cart++;
    },
    removeFromWishlist(book){
      let selected = this.wishlist.indexOf(book);
      this.wishlist.splice(selected, 1);
      this.cart--;
    } 
  },
  components: {
    NavbarComponent,CardComponent,TableComponent
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
