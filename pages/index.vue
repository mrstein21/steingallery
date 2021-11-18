<template>
 <div>
   <NavBar/>
    <div class="bg-white grid grid-cols-1 sn:grid-cols-2  md:grid-cols-3">
       <Gallery v-for="data in gallery" :key="data.id" :gallery="data"/>
    </div>
   <div class="mb-2 flex content-center items-center justify-center">
      <button    @click="prevPage"  :disabled="pageNumber <= 1" class="bg-red-600  text-white font-bold py-2 px-4 rounded-l">
        Prev
      </button>
        <button  @click="nextPage" :disabled="pageNumber >= totalPage"  class="bg-red-600   text-white font-bold py-2 px-4 rounded-r">
          Next
        </button> 
   </div>
 </div>
</template>
<script>
import Gallery from '../components/Gallery.vue'
import NavBar from '../components/NavBar.vue'
export default {
  components: { NavBar, Gallery },
  methods:{
    prevPage () {
      this.pageNumber--
      this.configurePage()
    },

    // Halaman selanjutnya
    nextPage () {
      this.pageNumber++
      this.configurePage()
    },
     configurePage () {
       location.href='/?page='+this.pageNumber
    }
  },
  data () {
    return {
      gallery:[],
      pageNumber: this.$route.query.page ? this.$route.query.page : 1,
    }
  },
  asyncData(context){
   return new Promise((resolve,reject)=>{
      var pageNumber=context.query.page ? context.query.page : 1
      console.log("halaman "+pageNumber);
      context.$axios.get("/v1/curated?page="+pageNumber+"&per_page=9",{
        headers:{
          "Authorization":process.env.API_KEY
        }
      }).then((resp)=>{
        context.gallery=resp.data.photos;
        resolve({
          gallery:resp.data.photos,
          totalPage:Math.ceil(resp.data.total_results/9)
        })
      })
    })
  }
}
</script>
