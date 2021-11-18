<template>
    <div  class="px-2 py-2"> 
        <div class="xl:max-w-xl">
            <!-- <img class="h-10" v-bind:src="'https://image.tmdb.org/t/p/w500'+row.poster_path" alt="Workcation" /> -->
            <img
            class="mt-5 rounded-lg  sm:mt-2 md-30 h-auto w-full  object-fill"
            v-bind:src="image" 
            alt="Woman workcationing on the beach"
            />
            <h1 
            class="text-sm md:text-base font-bold text-gray-900  lines mt-2 line-clamp-2"
            >
            {{resolution}}
            </h1>
      </div>
  </div>
</template>
<script>
export default {
    props:["resolution","image"],
}
</script>