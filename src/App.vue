<script setup>

</script>

<template>
  <div>
      <div class="px-4 py-2 py-20 w-[450px] ">
        <div class="rounded px-5   py-5 bg-gray-300 shadow hover:shadow-lg">
          <div class="flex justify-between item-center px-2 py-2 font-bold text-gray-400 hover:text-slate-600">
            <h1 class="text-center ">Votre note</h1>
            <i class="fas fa-notes-medical fa-2x"></i>
          </div>
          <div class="py-5 py-2">
          <form class="flex item-center space-x-4" @submit.prevent="add">
            <div class="relative">
              <input type="text"
               placeholder="entre votre note"
               autocomplete="off"
               name="note"  v-model="note" class="placeholder:text-blue-400  font-bold w-72 h-10 rounded-2xl indent-12 bg-gray-500">
               <i class="fas fa-address-card absolute left-2 top-5 font-bold text-gray-800 fa-lg"></i>
            </div>
            <div>
              <button
              type="submit"
               class="px-4 text-white font-bold rounded-2xl  hover:text-gray py-2 bg-gray-400 hover:bg-blue-400 roundex-2xl">
                 <i class="fas fa-plus"></i>
              </button>
            </div>
          </form>
        
          </div>
        </div>
        <div class="space-y-3 py-2 " >
        <div v-if="Object.keys(tasks).length===0" >
            <div class="flex justify-center items-center h-32 py-2 bg-gradient-to-r to-blue-400 from-yellow-100 rounded">
              <p class="font-bold text-gray-400">Aucun note pour vous</p>
            </div>
        </div>

          <div class="bg-gradient-to-r to-blue-400 from-sky-200 py-2" v-for="(task,index)  in tasks" :key="index" >
              <div class="grid grid-cols-12">
                <div class="col-span-8">
                    <div class="grid grid-cols-12 comic">
                      <div class="col-span-2 px-2 py-1">
                        <i class="fas fa-bookmark text-gray-400"></i>
                      </div>
                      <div class="col-span-10">
                        <p class="font-bold text-gray-600 petit py-2">{{task.title}} </p>
                      </div>
                    </div>
                </div>
                <div class="col-span-4 px-4">
                  <div class="flex justify-end item-center py-2 fa-lg space-x-4">
                    <i class="fas fa-trash text-gray-600 hover:text-white cursor-pointer" @click.prevent="supprime(index) "></i>
                    <i class="fas fa-edit text-gray-600 hover:text-white cursor-pointer" @click.prevent="edit(index) " ></i>
                  </div>
                </div>
              </div>
          </div>
        </div>
      </div>
      <div class="fixed  left-4 bottom-0 py-2">
        <p class="font-bold text-gray-400 space-x-4">
          <i class="fas fa-envelope-circle-check text-yellow-600"></i>
          email : <span class="underline text-stalte-600 cursor-pointer">randriatsilavinafrederic@0gmail.com</span>/
          <i class="fab fa-github text-blue-600"></i>
          github : <span class="underline text-stalte-600 cursor-pointer">fredericra</span>/
          <i class="fab fa-facebook text-sky-600"></i>
          facebook : <span class="underline text-stalte-600 cursor-pointer">eric randria</span>/
          <i class="fab fa-linkedin text-sky-600"></i>
          linkedln : <span class="underline text-stalte-600 cursor-pointer">eric randria</span>/
        </p>
      </div>
  </div>

</template>
<script>
import Swal from "sweetalert2";
export default {

  data()
  {
    return {
      tasks :
      [
        {title:"Back End : Developpeur laravel"},
        {title:"Laravel : Inertia ,Livewire "},
        {title:"FRONT END : Vue js , Tailwindcss, Bootstrap "},
        {title:"pack module node: sweelalert2,ziggy,aos scrool,fontawesome..."}
      ],
      note:'',
      editing:null,

    }
  },
  methods: {
    add()
    {

      if(this.note.lenght===0) return ;
      if(this.editing===null && this.note!=="")
      {
        this.tasks.push({title:this.note});
      this.note="";
       Swal.fire({
          title:"note ajouter success",
          icon:"success",
          timerProgressBar:true,
          timer:2000,
          toast:true,
          position:"top",
          showConfirmButton:false,
        })
      }
      else{
        this.tasks[this.editing].title=this.note;
        this.editing=null;
        this.note="";
        Swal.fire({
          title:"modification success",
          icon:"success",
          timerProgressBar:true,
          timer:2000,
          toast:true,
          position:"top",
          showConfirmButton:false,
        })
      
      }
      
    },
    supprime(id)
    {
      name=this.tasks[id].title;
       Swal.fire({
          title:"vous le vous-supprime ? <p class='text-sky-200'>" +name+"</p >",
          icon:"warning",
          position:"top",
          showConfirmButton:true,
          showDenyButton:true,
          confirmButtonText:"oui",
          denyButtonText:"non",
        }).then((request)=>{
          if(request.isConfirmed)
          {
             this.tasks.splice(id,1);
             Swal.fire({
              title:"suppression effectue !",
              icon:"success",
              toast:true,
              timerProgressBar:true,
              showConfirmButton:false,
            timer:2000,
              position:"top",
             })
          }
          else{
             Swal.fire({
              title:"suppression annuler !",
              toast:true,
              icon:"exclamation",
              timerProgressBar:true,
              showConfirmButton:false,
            timer:2000,
              position:"top",
             })
          }
        });
        this.note=""
    },
    edit(id)
    {
      this.editing=id;
      this.note=this.tasks[id].title;

    }

  },
}
</script>
<style >

</style>
