<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import { useScreen } from '@/composables/screen';
import CartPlus from 'vue-material-design-icons/CartPlus.vue';
import Account from 'vue-material-design-icons/Account.vue';
import Menu from 'vue-material-design-icons/Menu.vue';




const produtos = ref([]);
const { browserWidth, deviceWidth, isMobile } = useScreen();

onMounted(async () => {
  const response = await axios.get('https://fakestoreapi.com/products');
  produtos.value = response.data;
});

const formatPrice = (price) => `R$ ${price.toFixed(2).replace('.', ',')}`;
</script>

<template>
    <div>
      <h1 style="color: #FD8139;">
       Produtos - {{ browserWidth }} - {{ deviceWidth }} - {{
      isMobile}} 
      <span v-if="isMobile">É móvel</span>
    </h1>
      <div class="container">
        <div class="card" v-for="produto in produtos" :key="produto.id">
          <h1 class="card--title">{{ produto.title }}</h1>
           <!--<p>{{ produto.description }}</p>-->
           <p style="color: #FD8139;"  >{{ formatPrice(produto.price) }}</p>
          <img class="card--avatar" :src="produto.image" :alt="produto.title" />
        </div>
      </div>
      <div class="rodape-responsivo" v-if="isMobile" style="color: #FD8139;">
          <ul class="btn-rodape">
          <li><Account /></li>
          <li><CartPlus /></li>
          <li><Menu /></li>
        </ul>
      </div>
      <div class="rodape-descktop" style="background-color: #FD8139; color: white; text-align: center;" v-if="browserWidth >= 768">
        <footer>By: Laíssa Mendes</footer>
      </div>
    </div>
  </template>
  <style scoped>
  .container > .card > .card--title{
    color: #FD8139;
  }
  .container {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    justify-content: center;
    align-items: center;
    margin: auto;
    padding: 1rem 0;
  }
  .card {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-direction: column;
    width: 15rem;
    height: 25rem;
    background: #fff;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
    border-radius: 10px;
    margin: auto;
    overflow: hidden;
  }
  .card--avatar {
    width: 100%;
    height: 17rem;
    object-fit: cover;
    margin-bottom: 0.5rem;
  }
  .card--title {
    color: #222;
    font-weight: 700;
    text-transform: capitalize;
    font-size: 1.1rem;
    margin-top: 0.5rem;
  }
  .rodape-responsivo{
border-radius: 10px;
border-color: #FD8139;
border-style: solid;
box-shadow: 5px 5px 15px black;
  }
  @media (max-width: 768px) {
  .container {
    gap: 0.5rem;
  }
  .card {
    width: 92%;
  }
}

@media (min-width: 768px) and (max-width: 1024px) {
  .card {
    width: 22rem;
  }
}
  </style>