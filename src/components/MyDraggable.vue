<template>
  <draggable 
  ghost-class="opacity" 
  :sort="false" 
  :list="colors" 
  :class="[ ...myFlexContainer, 'my-4', 'mx-4']" 
  style="height: 40vh" 
  item-key="id" 
  :group="{ name: 'colors', pull: 'clone', put: false }"
  >
    <template #item="{ element }">
      <div :data-color="element.name" :class="['bg-' + element.name, 'col-md-2']" style="border-radius: 50%; min-height: 200px; max-width: 200px;"></div>
    </template>
  </draggable>
    <div :class="[ ...myFlexContainer, 'my-4', 'mx-4']" style="height: 40vh" >
  
  <div v-for="canva of canvas" :key="canva.id" class="h-50 col-2" style="min-height: 200px">       
   <draggable draggable="false" ghost-class="none" :class="[canva.color === null ? 'bg-dark' : '']" style="min-height: 200px;" @add="changeColor" v-model="canva.color" :data-canva="canva.id"  item-key="canva.id" group="colors">
      <template #item="{ element }">  
        <div :class="['bg-' + element, ...myFlexContainer]" style="min-height: 200px;">
          <span class="text-center text-white font-weight-bold h5">{{element}}</span>
        </div>
      </template>
    </draggable>
    </div>
  </div>

</template>

<script>
import draggable from 'vuedraggable'
import { squares, colors, myFlexContainer } from '../helpers/helper.js'
import { ref } from 'vue'

export default {
  name: "MyDraggable",
  components: {
    draggable,
  },
  setup(){
    const canvas = ref(squares)
      const changeColor = (evt) => {
        const color = evt.item.attributes['data-color'].value
        const id = evt.to.attributes['data-canva'].value
        
        const idx = canvas.value.map(canva => canva.id).indexOf(+id)

      canvas.value[idx].color = [color]
    }

    return { colors, canvas, changeColor, myFlexContainer }
  }
}
</script>
<style scoped lang="css">
.opacity {
  opacity: 0;
}
.none {
  display: none;
}
</style>
