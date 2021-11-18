<template>
 <div>
    <NavBar/>
    <div class="bg-white grid  grid-cols-1 lg:grid-cols-3 md:grid-cols-3">
        <div class="px-8 lg:col-span-2 md:col-span-2 py-8">
            <img
            class="mt-2 rounded-lg shadow-xl  h-auto w-full  object-fill"
            v-bind:src="gallery.src.original"/>
            <h1
            class=" mt-2 text-base md:text-2xl font-bold text-gray-900"
            >
            {{gallery.photographer}}
            </h1>
            <h1
            class=" mt-2 text-base md:text-xl font-bold text-gray-900"
            >
             Resolution
            </h1>
             <div class="grid grid-cols-2 md:grid-cols-3">
                <Resolution v-for="(data,key) in gallery.src" :key="key" :image="data"  :resolution="key"/>
             </div> 
        </div>
    </div>
 </div>    
</template>
<script>
import Resolution from '../../components/Resolution.vue';
export default {
  components: { Resolution },
    asyncData(context){
     return new Promise((resolve,reject)=>{
      context.$axios.get("/v1/photos/"+context.params.id,{
        headers:{
          "Authorization":process.env.API_KEY
        }
      }).then((resp)=>{
        resolve({
          gallery:resp.data,
        })
      })
    })
  }
}
</script>