<template>
 <a :href="'/'+gallery.id">
    <div class="px-5 py-4 max-w-md mx-auto sm:max-w-xl  lg:max-w-full xl:mr-0 2xl:col-span-2" >
      <div class="xl:max-w-xl">
        <img
          class="mt-5 rounded-lg shadow-xl h-auto sm:mt-2   w-full  object-cover"
          v-bind:src="gallery.src.original" 
        />
        <h1 class="mt-2  font-bold text-gray-900 text-sm md:text-lg ">
          {{gallery.photographer}}
        </h1>
      </div>
    </div>
 </a> 
</template>
<script>
export default {
    props:["gallery"]
}
</script>