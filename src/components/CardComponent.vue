<template>
    <div class="d-flex flex-wrap justify-content-between">
        <div
          v-for="book in books"
          :key="book.ISBN"
          v-show="!isVisible"
          class="card fs-5 p-3 m-2"
          style="width: 25rem"
        >
          <img :src="book.image" class="card-img-top" style="height: 30rem" />
          <div class="card-body">
            <div class="row">
              <p class="card-text d-inline col">{{book.category}}</p>
              <p class="card-text d-inline col">{{book.author}}</p>
            </div>
            <div class="row">
              <p :class="[book.pages < 50 ? 'less' : 'more']" class="card-text d-inline col">
                Pages: {{book.pages}}
              </p>
              <p class="card-text d-inline col">{{currencyFormat(book.price.displayValue)}}</p>
            </div>
            <div class="row">
              <p class="card-text d-inline col">{{book.ISBN}}</p>
              <button
                class="btn btn-primary col"
                @click="addToWishlist(book)"
                :disabled="disableButton(book)"
              >
                Add to wishList
              </button>
            </div>
          </div>
        </div>
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
          addToWishlist(book) {
            this.$emit('add-to-wishlist', book);
          },
          disableButton(book) {
            return this.wishlist.some(item => item.book.ISBN === book.ISBN);
          },
          currencyFormat(price) {
            return Intl.NumberFormat('ar-SA', {
              style: 'currency',
              currency: 'SAR',
              maximumFractionDigits: 0,
            }).format(price);
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
.more {
        color: green;
      }

      .less {
        color: orangered;
      }

      .more,
      .less {
        font-weight: bold;
      }
</style>