<template>
    <div id="app" v-cloak>
          <div class="myList">
            <table v-if="lists.length">
              <thead>
                <tr>
                  <th>lp.</th>
                  <th>produkt</th>
                  <th>ilość</th>
                   <th>usuń</th>
                </tr>
              </thead>

              <tbody>
                <tr v-for="(list, index) in lists" >
                  <td>{{index+1}}.</td>
                  <td>{{list.product}}</td>
                  <td class="quantity"><div @click="minus(index)">-</div>{{list.quantity}}<div @click="plus(index)">+</div></td>
                  <td @click="remove(index)"><i class="fas fa-trash-alt"></i></td>
                </tr>
              </tbody>
          </table>
          <div class="empty" v-else>
            <p>brak zakupów</p>
          </div>
          </div>
          <input type="text" placeholder="wpisz produkt" v-model.trim="product">
          <input id="number" type="number" value="1" placeholder="0" min="1" v-model.number="quantity">
          <button :disabled="!isFilled" @click="add">dodaj</button>
        </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  data: function(){
    return {
              product: '',
              quantity: '',
              lists: [],
      }
    },
    computed:{
              isFilled: function(){
                return this.product && this.quantity>0;
              }
            },
     methods: {
              add: function(){
               this.lists.push(
                    {product: this.product, quantity: this.quantity}
                  );
                  this.product="";
                  this.quantity ="";
              },
              remove: function(index){
                this.lists.splice(index, 1);
              },
              plus: function(index){
                this.lists[index].quantity++
              },
              minus: function(index){
               
                if(this.lists[index].quantity<=1){
                  return false;
                }else{ this.lists[index].quantity--;}
              },
            },
    components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
html{
  font-size: 62.5%;
}
thead tr th{
  padding: 1rem 4rem;
  font-size: 1.6rem;
  font-weight: bold;
}
tbody tr td{
  font-size: 1.6rem;
  padding: 1rem;
}

.myList{
  display: block;
}
table{
  margin: 0 auto;
}
.empty{
  font-size: 1.6rem;
}
input[type="text"]{
  width: 22%;
}
input[type="number"]{
  width: 5%;
}

.quantity div{
  display: inline-block;
  padding: 0.1rem 0.6rem;
  font-size: 1.6rem;
  font-weight: bold;
  border: 1px solid black;
  margin: 0 1.5rem;
  border-radius: 10px;

}
</style>
