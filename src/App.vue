<template>
<div class="wrapper">
  <div>第 {{n}} 手</div>
  <div class="chess">
  <div class="row">
    <Cell @click="onClickCell(0,$event)" :n="n"/>
    <Cell @click="onClickCell(1,$event)" :n="n"/>
    <Cell @click="onClickCell(2,$event)" :n="n"/>
  </div>
  <div class="row">
    <Cell @click="onClickCell(3,$event)" :n="n"/>
    <Cell @click="onClickCell(4,$event)" :n="n"/>
    <Cell @click="onClickCell(5,$event)" :n="n"/>
  </div>
  <div class="row">
    <Cell @click="onClickCell(6,$event)" :n="n"/>
    <Cell @click="onClickCell(7,$event)" :n="n"/>
    <Cell @click="onClickCell(8,$event)" :n="n"/>
  </div>
  </div>
  <div>{{result}}</div>
</div>
</template>

<script>
import Cell from "./Cell";
export default{
  components:{Cell},
  data(){
    return{
    n:0,
    map:[
      [null,null,null],
      [null,null,null],
      [null,null,null]
    ],
    result:'比赛进行中...'
  };
  },
  methods:{
    onClickCell(i,text){
      console.log(`第${i}个cell被点了,内容是:${text}`)
      this.map[Math.floor(i/3)][i%3]= text;
      this.n++;
      this.tell()
    },
    tell(){
      const map = this.map
      //横
      for(let i=0;i<2;i++){
        if(map[i][0] !== null && map[i][0] === map[i][1] && map[i][1] === map[i][2]){
          this.result =  map[i][0]+' 获胜了';
        }
      }
      //竖
      for(let j=0;j<2;j++){
        if(map[0][j] !== null && 
           map[0][j] === map[1][j] && 
           map[1][j] === map[2][j]){
          this.result =  map[0][j]+' 获胜了';
        }
      }
      //对角线
      if(map[0][0] !== null && map[0][0] === map[1][1] && map[1][1] === map[2][2]){
        this.result = map[0][0]+' 获胜了';
      }

      //对角线
      if(map[0][2] !== null && map[0][2] === map[1][1] && map[1][1] === map[2][0]){
        this.result = map[0][2]+' 获胜了';
      }

    }
  }
};
</script>

<style>
.row{
  display:flex
}
.wrapper{
    display:flex;
    justify-content:center;
    align-items:center;
    flex-direction:column;
}
</style>
