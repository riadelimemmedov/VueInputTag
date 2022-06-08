<template>
  <div class="tag-container">
    <app-tag v-for="tag in tags" :key="tag" :tag="tag" :tagColor="color" @selectedDeleteTag="deletedClick($event)"></app-tag>
    <!-- <input type="text"   v-on:keyup.enter="tags.push($event.target.value)"> -->
    <!-- ! Or @keydown.enter -->
    <input type="text" @keydown.enter="addTags($event)" @keydown.backspace="deleteTag($event)"><br><br>
    <div class="error" v-if="error">Bu etiket daha onceden eklenmis</div>
  </div>
</template>

<script>
  import Tag from './Tag.vue'
  export default{
    data(){
      return{
        tags:[],
        message : '',
        error:false
      }
    },
    methods:{
      addTags(added_tag){
        let addedText = added_tag.target.value
        console.log('Added Text Lenght ', addedText.length)
        let matchData = true

        if(addedText.length > 0){
          this.tags.forEach((tag)=>{
            if(tag.toLowerCase() == addedText.toLowerCase()){
              matchData = false
            }
          })
          if(matchData == true){
                this.tags.push(addedText)
                // this.$emit('input',this.tags.join(','))
                //Or watch methods
                added_tag.target.value = ''
              }
            else{//matchData == false
              this.error = true
              setTimeout(()=>{
                this.error = false
              },2000)
            }
        }
        else if(addedText.length == 0){
          alert('Lutfen input alanina deger girin')
        }
      },
      deleteTag(deleted_tags){
        if(deleted_tags.target.value.length <= 0){
          // this.tags.pop()
          //Or
          this.tags.splice(this.tags.length-1,1)
        }
      },
      deletedClick(e){
        //console.log(e.target.previousSibling.previousSibling.textContent)
        let deleted_tag_text = e.target.previousSibling.previousSibling.textContent
        if(this.tags.includes(deleted_tag_text)){
          console.log(this.tags.indexOf(deleted_tag_text))
          this.tags.splice(this.tags.indexOf(deleted_tag_text),1)
        }
      }
    },
    components:{
      'app-tag':Tag
    },
    props:{
      value:{//tags value from App.vue components in data
        required:false
      },
      color:{
        type:String,
        required:false,
        default:"primary"
      }
    },
    watch:{
      tags(){
        this.$emit('input',this.tags.join(','))
      }
    },
    created(){
      if(this.value){
        if(this.value.length > 0){
          this.tags = this.value.split(',')
        }
      }
    }
  }
</script>

<style scoped>
    .tag-container{
      border: 1px solid #ccc;
      padding: 20px;
      margin-top: 10px;
    }
    .error {
      font-size: 12px;
      font-weight: bold;
      color: red;
      margin-top: 1px;
    }

    input {
      outline: none;
      height: 30px;
      width: 120px;
    }

</style>
