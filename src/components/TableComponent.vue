<template>
    <div class="text-center m-2" v-show="isVisible">
        <h4 class="py-2" v-show="wishlist.length == 0">Sorry you have no books in your wishList</h4>
        <table class="table" v-show="wishlist.length > 0">
          <thead>
            <tr class="fs-3">
              <th scope="col">ISBN</th>
              <th scope="col">Title</th>
              <th scope="col">Author</th>
              <th scope="col">Price</th>
              <th scope="col">Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in wishlist" :key="item.book.ISBN" class="fs-4">
              <th scope="row">{{item.book.ISBN}}</th>
              <td>{{item.book.title}}</td>
              <td>{{item.book.author}}</td>
              <td>{{currencyFormat(item.book.price.displayValue)}}</td>
              <td>
                <button class="btn btn-danger" @click="removeFromWishList(item)">
                  Remove from wishlist
                </button>
              </td>
            </tr>
          </tbody>
          <tfoot>
            <tr class="fs-4">
              <th colspan="3">Total Price</th>
              <td colspan="3">{{currencyFormat(total())}}</td>
            </tr>
          </tfoot>
        </table>
      </div>
</template>
<script>
import { booksData } from "../book";
export default {
    data() {
          return {
            books: booksData,
          };
        },
        methods: {
          removeFromWishList(book) {
            this.$emit('remove-from-wishlist', book);
          },
          currencyFormat(price) {
            return Intl.NumberFormat('ar-SA', {
              style: 'currency',
              currency: 'SAR',
              maximumFractionDigits: 0,
            }).format(price);
          },
          total() {
            let totalPrice = 0;
            for (let i = 0; i < this.wishlist.length; i++) {
              totalPrice += this.wishlist[i].book.price.value;
            }
            return totalPrice;
          },
        },
        props:{
        isVisible:{
          type:Boolean
        },
        wishlist:{
          type:Array
        }
    }
}
</script>
<style scoped>

</style>