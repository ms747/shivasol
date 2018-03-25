<template >      
            <li v-if="isBrand == false" class="menu-item mobile" >
                {{name.title}}
            </li>
            <li v-else class="menu-item site-branding">
                {{name.title}}
            </li>
</template>

<script>
export default {
    data : function(){
        return{
            
        }
    },
    props : ['name','isBrand']
}
</script>

<style>

</style>
