<template>
  <div class="container">
    <div class="text-box">
      <p><span>
        Пусть 2020 год принесёт еще больше хороших и интересных событий, о которых ты будешь
        вспоминать с улыбкой; пусть будет меньше стресса и больше теплых и ламповых моментов;
        пусть каждый новый день у тебя будет хорошим и вызывать улыбку.
        Сердечно тебя обнимаю:) С Новым годом!
        <br>А ниже мини-подборка из наших моментов, какие у меня были сохранены :D
      </span></p>
    </div>
    <div class="box"><p/></div>
    <div>
      <table>
        <tbody>
          <tr>
            <td align="right">
              <div>
                <a class="prev" @click="prev" href="#">&#10094; Previous</a>
              </div>
            </td>
            <td>
              <div>
                <transition-group name="fade" tag="div">
                  <div :key="currentInd" class="box">
                    <router-link :to="`/photo/${images[currentInd].id}`">
                      <img v-if="currentInd > 1" class="rotate"
                           :src="thumbUrl(images[currentInd].filename)"/>
                      <img v-if="currentInd <= 1"
                           :src="thumbUrl(images[currentInd].filename)"/>
                    </router-link>
                  </div>
                </transition-group>
              </div>
            </td>
            <td align="left">
              <div>
                <a class="next" @click="next" href="#">Next &#10095;</a>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="box">
      <footer>Корпорация "Всратые папарацци"<br>Студия "Лапки CSS"</footer>
    </div>
  </div>
</template>


<script>
import photos from '@/photos.json';
import { store } from '../store';

export default {
  name: 'Slider',
  data() {
    return {
      images: photos,
      timer: null,
      currentInd: store.state.currentPhoto,
    };
  },

  mounted() {
    this.startSlide();
  },

  methods: {
    imageUrl() {
      return require('../assets/images/christmas_snow.jpg');
    },
    thumbUrl(filename) {
      return require(`../assets/images/thumbnails/${filename}`);
    },
    startSlide() {
      this.timer = setInterval(this.next, 10000);
    },
    next() {
      if (this.currentInd + 1 === this.images.length) {
        this.currentInd = 0;
      } else {
        this.currentInd += 1;
      }
      store.setPhoto(this.currentInd);
    },
    prev() {
      if (this.currentInd - 1 < 0) {
        this.currentInd = this.images.length - 1;
      } else {
        this.currentInd -= 1;
      }
      store.setPhoto(this.currentInd);
    },
  },

  computed: {
    currentImg() {
      return this.images[this.currentInd];
    },
  },
};
</script>

<style scoped>
  .fade-enter-active,
  .fade-leave-active {
    transition: all 0.5s ease;
    overflow: hidden;
    visibility: visible;
    position: relative;
    width:100%;
    opacity: 1;
  }

  .fade-enter,
  .fade-leave-to {
    visibility: hidden;
    width:100%;
    opacity: 0;
  }

  .box {
    display: flex;
    justify-content: center;
  }

  .text-box {
    width: 35%;
    height: fit-content;
    padding: 10px;
    line-height: 30px;
    font-max-size: 30px;
    font-min-size: 12px;
    text-align-all: center;
    background-color: white;
    border-radius: 16px;
    box-shadow: 2px 2px 4px black;
    margin: 0 auto;
    background-clip: padding-box;
    word-wrap: break-word;
    white-space: normal;
    border-style: solid;
    border-color: aquamarine;
    border-width: medium;
  }

  .container {
    background-image: url('../assets/images/christmas_snow.jpg');
    width: 100%;
    height: 900px;
  }

  img {
    height:400px;
    width:100%;
    border-radius: 5%;
    box-shadow: 3px 3px 4px black
  }

  table {
    table-layout: fixed;
    width: 100%;
  }

  footer {
    text-align: left;
    position: absolute;
    bottom: 0;
    left: 20px;
    width: 100%;
    height: 0;
  }

  .rotate {
    transform-origin: center;
    transform: rotate(90deg);
  }

  .prev, .next {
    cursor: pointer;
    position: relative;
    top: 40%;
    width: auto;
    padding: 16px;
    color: black;
    font-weight: bold;
    font-size: 18px;
    transition: 0.5s ease;
    border-radius: 10%;
    text-decoration: none;
    user-select: none;
  }

  .prev:hover, .next:hover {
    background-color: white;
    box-shadow: 3px 3px 4px black
  }
</style>
