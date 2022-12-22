<template>
    <div>
        <div class="flex vignette-shadow-ex justify-start columns-1 pl-10" v-if="url" id="preview" v-bind:style="{
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

        <div class="p-10">
            <div class="mb-6">
                <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">
                    หัวข้อ</label>
                <input type="text" v-model="title"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
            </div>

            <div class="mb-6">
                <label  class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">
                    คำอธิบาย</label>
                <textarea type="text" v-model="subtitle"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
                </textarea>
            </div>
        </div>

    </div>
</template>

<script>
export default {
    data() {
        return {
            url: null,
            height: null,
            width: null,
            title: 'หัวข้อ',
            subtitle: 'คำอธิบาย',
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
        updateTitle(e) {
            console.log(e);
        },
        updateSubTitle(e) {
            console.log(e);
        }
    },
}
</script>
<style>
.vignette-shadow-ex {
    max-height: 500px;
    max-width: 500px;
    box-shadow: inset 0 -170px 50px black;
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center center;
}

.text-box {
    height: 90px;
    width: 420px;
}
</style>