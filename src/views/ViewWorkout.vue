<script setup>
import {ref} from 'vue';
import supabase from '../supabase/init';
import {useRoute} from 'vue-router'

const route = useRoute()

const data = ref(null)
const dataLoaded = ref(null)
const errorMsg = ref(null)
//const statusMsg = ref(null)
//2:23

const currentId = route.params.workoutId

const getData = async() => {
  try{
    const {data: workouts, error} = await supabase.from('workouts').select('*').eq('id', currentId)
    if(error) throw error
    data.value = workouts
    dataLoaded.value = true
    console.log(data.value)
    
  }catch(error){
    errorMsg.value = error.message
    setTimeout(() => {
      errorMsg.value = false
    }, 5000)
  }
}

getData()
console.log(data.value)

</script>

<template>
  <div></div>
</template>


