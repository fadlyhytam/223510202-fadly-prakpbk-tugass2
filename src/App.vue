<template>
  <div>
    <h1 :class="{ 'bold-text': isBold }" :style="{ fontSize: fontSize + 'px' }">
      <transition name="text-color">
        <span :class="{ 'red-text': isRed }">Hello, {{ name }}!</span>
      </transition>
    </h1>
    <input type="text" v-model="name" @input="checkNameLength" />
    <button @click="saveInput">Simpan Input</button>
    <ul>
      <li v-for="(input, index) in savedInputs" :key="index">
        <span :class="{ 'red-text': input.length > 5 }">{{ input }}</span>
        <button @click="deleteInput(index)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: 'World',
      isRed: false,
      isBold: false,
      fontSize: 16,
      savedInputs: []
    }
  },
  methods: {
    checkNameLength() {
      if (this.name.length > 5) {
        this.isRed = true
        this.isBold = true
        this.fontSize = 20 // Mengubah ukuran font saat teks lebih dari 5 karakter
      } else {
        this.isRed = false
        this.isBold = false
        this.fontSize = 16 // Mengembalikan ukuran font ke nilai awal
      }
    },
    saveInput() {
      this.savedInputs.push(this.name)
    },
    deleteInput(index) {
      this.savedInputs.splice(index, 1)
    }
  }
}
</script>

<style>
.red-text {
  color: red;
}
.bold-text {
  font-weight: bold;
}
.text-color-enter-active,
.text-color-leave-active {
  transition: color 0.5s;
}
</style>
