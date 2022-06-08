<template>
  <span class="tag" :class="selectedTheme">
    <span class="content-tag">{{ tag }}</span>
    <span class="close-tag" @click="$emit('selectedDeleteTag',$event)">X</span>
  </span>
</template>

<script>
  export default{
    data(){
      return{
        isColor:false,
        selectedTheme:null
      }
    },
    props:['tag','tagColor'],
    created(){
      this.selectedTheme = this.tagColor
    }
  }
</script>

<style scoped>
  .primary{
    color:#004085;
    background-color: #cce5ff;
    border-color: #b8daff;
  }

  .tag {
    padding: 10px;
    cursor: default;
    margin-right: 8px;
  }
  .tag * {
    font-size: 14px;
  }

  .tag .close-tag {
    font-size: 12px;
    cursor: pointer;
  }
</style>
