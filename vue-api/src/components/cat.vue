<template>
    <div class="wrap">
      <h1>고냥이(api 연동)</h1>
      <div class="box-img"><img :src="catImgUrl" alt=""></div>
      <!-- <button type="button" class="btn" @click="getCat">귀여운 고양이 봐주세요</button> -->
      <div class="wrap-btn">
        <button type="button" @click="getPrev">prev</button>
        <button type="button" @click="getNext">next</button>
      </div>
    </div>
</template>

<script>
  import { ref, onMounted } from 'vue'
  import axios from 'axios'


  export default {
    setup() {
      const catImgUrl = ref('');
      const catImages = ref([]); // 이미지 배열 (순서대로 노출되게끔 배열로 정리..)
      let currentImgIndex = 0;

      const getPrev = () => {
        if (currentImgIndex > 0) {
          currentImgIndex--;
          catImgUrl.value = catImages.value[currentImgIndex];
        }
      };

      const getNext = () => {
        if (currentImgIndex < catImages.value.length - 1) {
          currentImgIndex++;
          catImgUrl.value = catImages.value[currentImgIndex];
        } else {
          axios.get('https://api.thecatapi.com/v1/images/search')
            .then((response) => {
              const imgUrl = response.data[0].url;
              catImgUrl.value = imgUrl;
              catImages.value.push(imgUrl); // 이미지 URL을 배열에 저장
              currentImgIndex = catImages.value.length - 1;
            })
            // .catch((error) => {
            //   console.error('고양이 이미지 에러', error);
            // });
        }
      };

      onMounted(() => {
        getNext(); // 컴포넌트가 마운트될 때 호출
      });

      return { catImgUrl, currentImgIndex, getPrev, getNext }
    }
  }
</script>

<style scoped>
</style>
