<template>
  <div>
    <div class='cell' v-on:click="onClickSelf">
      <template v-if="a">
        {{text}}
      </template>
      <template v-else > 
      </template>
    </div>
    </div>
</template>

<script>
export default{
  //接收App.vue传过来的n   :n="n"   bind和props用法
  props:["n"],
  data(){
    return{a:false,text:""}
  },
  methods:{
    onClickSelf(){
      if(this.text !== ""){
        return;
      }
      this.a =  true;
      //判断是 x 还是 o
      this.text = this.n %2 === 0?"x":"o";
      //告诉外界 我被点了,并把x或o传出去 App.vue中触发Cell的点击事件
      this.$emit("click",this.text);
  }
}
};
</script>


<style>
.cell{
  border:1px solid black;
  width:100px;
  height:100px;

  /* 文字居中 */
  display:flex;
  justify-content:center;
  align-items:center;

  font-size:80px;
}
</style>
