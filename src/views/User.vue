<template>
    <div>
        <h1>User List</h1>
        <HelloWorld  :msg="message" ></HelloWorld>

    </div>
</template>
<script>
import HelloWorld from '@/components/HelloWorld.vue'
export default {
     name: 'User',
  components: {
    HelloWorld
  },
  data(){
      return{
          message: 'WYEEEEEEEEEEEEE'
      }
  }
}
</script>
