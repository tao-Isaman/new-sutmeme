<template>
  <div>
    <div id="capture" class="flex justify-start columns-1 pl-10 vignette-shadow-ex" :class="{
      'vignette-shadow-ex': real ,
      }" v-if="url" v-bind:style="{
      'background-image': 'url(' + url + ')',
      'height': height + 'px',
      'width': width + 'px',
    
    
    }">
      <div class="grid grid-cols-1 content-end">
        <div>
          <p class="text-amber-600 title-meme">{{ title }}</p>
          <p class="text-white sub-title-meme text-box">{{ subtitle }}</p>
        </div>
      </div>

    </div>
    <span>Upload to image</span>
    <input type="file" accept=".jpeg,.jpg,.png,image/jpeg,image/png" aria-label="upload image button"
      @change="uploadImg" />

    <div class="grid p-10 ">
      <div class="mb-3">
        <label class="block mb-2 font-medium text-gray-900 dark:text-white">
          หัวข้อ</label>
        <input type="text" v-model="title"
          class="bg-gray-50 border border-gray-300 text-gray-900  focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
      </div>

      <div class="mb-3">
        <label class="block mb-2 font-medium text-gray-900 dark:text-white">
          คำอธิบาย</label>
        <textarea type="text" v-model="subtitle"
          class="bg-gray-50 border border-gray-300 text-gray-900  focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
              </textarea>
      </div>

      <button @click="printThis"
        class="mb-3 justify-self-center text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Submit</button>

    </div>

  </div>
</template>

<script>
import html2canvas from 'html2canvas';
export default {
  data() {
    return {
      url: null,
      height: null,
      width: null,
      title: 'หัวข้อ',
      subtitle: 'คำอธิบาย',
      real: true,
    }
  },
  methods: {
    async uploadImg(e) {
      const file = e.target.files[0];
      this.url = URL.createObjectURL(file);
      let img = new Image();

      img.onload = () => {
        this.height = img.height;
        this.width = img.width;
      }
      img.src = this.url;
    },
    printThis() {
      html2canvas(document.querySelector("#capture")).then(canvas => {
      document.body.appendChild(canvas)
    });
    }
  }
}
</script>
<style>

.vignette-shadow-ex {
  max-height: 500px;
  max-width: 500px;
  box-shadow: inset 0 -150px 50px black;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center center;
}

.text-box {
  height: 90px;
  width: 420px;
}
</style>