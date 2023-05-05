<template>
  <form @submit.prevent="addUser">
      <input type="text" v-model="state.newUser" placeholder="Enter a name">
      <button type="submit">Add User</button>
  </form>
  <draggable v-model="state.users"  @end="onDragEnd">
    <template #item="{ element }">
      <div class="list-item">
        {{ element.name }}
      </div>
    </template>
  </draggable>
</template>



<script lang="ts">
  import { defineComponent, reactive } from 'vue';
  import draggable from 'vuedraggable';

  export default defineComponent({
    components: { draggable },
    setup() {
      const state = reactive({
        users: [
          { id: 1, name: 'John Doe', position: 1 },
          { id: 2, name: 'Jane Smith', position: 2  },
          { id: 3, name: 'Bob Johnson', position: 3  },
        ],
        newUser: '',
      });
      
      const addUser = () => {
        if(state.newUser.length > 0){
          state.users = [...state.users, { id: (new Date()).getTime(), name: state.newUser, position: 4 }]
          state.newUser = ''          
        }

      };


      const onDragEnd = (event: any)  =>{
        console.log("Element at index " + event.oldIndex + " was dragged to index " + event.newIndex);
        console.log(2222, state.users)
      }



      return { state, addUser, onDragEnd };
    }
  });
</script>

<style>
  .list-item{
    background-color: aqua;
    margin: 10px 0;
    padding: 10px;
  }
</style>



