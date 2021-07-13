<template>
  <header>
      <a href="/">
        <img src="../assets/images/logo.png" alt="Logo Boolflix">
      </a>
      <div>
          <input 
            v-model="searchText"
            type="text" 
            placeholder="Cerca il tuo film preferito"
            @keyup.enter="$emit('performSearch', searchText)"  
            >
          <button
            @click="$emit('performSearch', searchText)"
          >Cerca</button>
      </div>
  </header>
</template>

<script>
export default {
    name: "Header",
    data: function() {
        return {
            searchText: ''
        }
    }
}
</script>

<style lang="scss" scoped>
    header {
        display: flex;
        justify-content: space-between;
        padding: 0 15px;
    }
</style>