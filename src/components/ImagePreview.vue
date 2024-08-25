<template>
  <div class="container">
    <div class="image-picker-container">
      <!-- the user selects an image -->
      <v-file-input v-if="!image" class="img-input-cont" type="file" accept="image/*" hide-details variant="outlined"
        @change="selectImg" v-model="image" rounded="xl" prepend-icon="undefined">
        <template v-slot:label="{ isActive }">
          <div>
            <div class="img-input-label">
              <div class="img-upload-icon" v-if="!isActive.value">
                <v-icon icon="mdi-cloud-upload"></v-icon>
              </div>
              <div class="img-upload-text">
                <p>select an image to upload</p>
              </div>
            </div>
          </div>
        </template>
      </v-file-input>

      <!-- A preview only shows if the user has selected an image -->
      <div class="preview-img-cont" v-if="image">
        <img v-if="image" :src="imageUrl" alt="" />
        <v-icon class="preview-close-btn" icon="mdi-close-circle-outline" size="large"
          @click="image = undefined"></v-icon>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">

import { ref } from "vue"

const imageUrl = ref()
const image = ref()




/* a function that renders the selected image */
const selectImg = () => {
  const file = image.value
  if (file) {

    const reader = new FileReader();
    reader.onload = e => {
      if (e.target) imageUrl.value = e.target.result;
    };
    reader.readAsDataURL(file);
  }
}
</script>
<style>
.img-upload-icon>img {
  width: 3rem;
}

.image-picker-container {
  overflow: hidden;
  height: 20rem;
  max-width: min(100%, 800px);
  width: 100%;
}

.preview-img-cont {
  position: relative;
  height: 100%;
  width: 100%;
  border-radius: 24px !important;
  border-width: 1px;
  border-style: solid;
  border-color: #e5e7eb;
  overflow: hidden;
}

.preview-img-cont img {
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  min-width: 100%;
  min-height: 100%;
}

.preview-close-btn {
  position: absolute !important;
  top: 10px;
  right: 10px;
  color: var(--accent);
  cursor: pointer;
}

.next-btn {
  position: absolute;
  left: 50%;
  transform: translate(-50%, 0);
  bottom: 10px;
  border-width: 1px;
  background: var(--primary);
  opacity: 0.9;
  color: white;
}

.img-input-cont {
  display: flex !important;
  justify-content: center;
  min-height: 20rem;
  max-width: min(100%, 800px);
  width: 100%;
  text-align: center;
}

.img-input-label {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.img-input-cont .v-label {
  width: 100%;
}

.container {
  margin: 0 auto;
  margin-top: 1rem;
  margin-bottom: 3rem;
  max-width: min(35rem, 90%);
  gap: 3.5rem;
  display: flex;
  flex-direction: column;
}

.v-input__control {
  width: 100% !important;
}
</style>
