<script setup>
import { ref} from 'vue'

let items = ref([{ id: 0,
    title: 'Foo: ',
    img: 'https://news.artnet.com/app/news-upload/2019/01/Cat-Photog-Feat-256x256.jpg',
    desc: 'lorem ipsum sit dolor amed ipsum sit dolor amed ipsum sit dolor amed '
  },])

function addItem(title,img,desc){
  if (title!=undefined){title+=': '}else{title=''}
  let object = {id:1,title:title,img:img,desc:desc}

  items.value.push(object)
  
  //localStorage.setItem('items',JSON.stringify(items.value))
}
</script>

<template>
    <form class="menu-wrapper" @submit.prevent='addItem(title,url,desc)' autocomplete="off">
      <button class='addButton' type="submit">Add new Item</button><br>
      <input id='title' class="input" v-model="title" placeholder="title (optional)" />
      <input type="url" id='url' class="input" v-model="url" required="required" pattern="https://.*" placeholder="image url" />
      <textarea id='desc' class="input description" required="required" v-model="desc" placeholder="Description" maxlength="500"></textarea>
    </form>
  <div class="grid-wrapper">
    <div
      class="list-item"
      v-for="items in items"
      :key="items.id"
    >
      <img v-bind:src='items.img'><br>
      <span class="title">{{items.title}}</span>
      <span>{{items.desc}}</span>
    </div>
  </div>
</template>

<style>
html, body {
  height: 100%;
  font-family: Arial, Helvetica, sans-serif;
}
#app {
  height: 100%;
}

.menu-wrapper {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;

  max-width: 500px;
  margin: 15px auto;
}

.input {
  flex-basis: 100%;
  margin:5px 0;
  resize: none;
}

.input.description {
  display: inline-block;
  height: 100px;
}

.grid-wrapper{
  height: 100%;
  border: solid black 1px;

  display: grid;
  grid-template-columns: repeat(auto-fill, 200px);
  grid-template-rows: repeat(auto-fill, 250px);
  gap: 10px;
  justify-items: center;
  justify-content: center;
  
  margin: 0 auto;
  padding: 5px;
}

.list-item {
  width: 150px;
  height: 200px;

  padding: 5px;

  text-align: center;

  overflow: hidden;
  text-overflow: ellipsis;
}

.list-item img {
  object-fit: contain;
  width: 100%;
  height: 100px;

  filter: drop-shadow(0 0 2px gray);
}

.list-item .title {
  font-weight:bold;
}
</style>