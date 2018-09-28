<template>
  <div>
    <input type="text" v-model="text"/>
    <div class="lesson-list">
      <div 
        class="lesson" 
        v-for="(lesson,idx) in lessons" 
        :key="lesson[idx]"
      >
        <h2>{{lesson.title}}</h2>
      </div>
    </div>
  </div>  
</template>


<script>
  import debounce from 'lodash/debounce';
  const SearchAPI = 'https://hiskio.com/api/v1/courses/search?word=';
  export default {
    data(){
      return {
        text:'',
        lessons: [],
      }
    },
    methods:{
      search(val){
        fetch(`${SearchAPI}${val}`)
        .then(rs => rs.json())
        .then(data => this.lessons = data.courses);
      },
    },
    watch:{
      text(val){
        this.searchDebounced(val);
      }
    },
    created() {
      this.searchDebounced = debounce(this.search, 800);
    },
  }
</script>


<style>

</style>

