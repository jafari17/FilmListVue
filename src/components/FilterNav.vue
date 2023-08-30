
<template>

  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{active: current === 'all'}"> view all</button>
    <button @click="updateFilter('star')" :class="{active: current === 'star'}"> star</button>
    <button @click="updateFilter('non-star')" :class="{active: current === 'non-star'}" >non-star</button>
  </nav>
</template>



<script >
export default {
  props:['current'],
  methods:{
    updateFilter(by){
      this.$emit('filterChange', by)

    }
  }
}

</script>



<style >
.filter-nav button{
  background: none;
  border: none;
  color: #888888;
  outline: none;
  font-size: 16px;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button.active{
  color: #000000;
}
</style>