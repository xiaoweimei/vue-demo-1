<template>
  <div class="wrapper">
    <h3>简介：Vue井字棋；author: xiaoweimei</h3>
    <h4 :style="{color:'red'}">规则：先手为x,后手为o,先占据一行(或列或对角线)者为胜者</h4>
    <h2 v-if="result===null">开始第{{n+1}}手，落子方为{{n%2===0?'x':'o'}}</h2>
    <div class="chess">
    <div class="row">
      <cell @click="onClickCell(0,$event)" :n="n"/>
      <cell @click="onClickCell(1,$event)" :n="n"/>
      <cell @click="onClickCell(2,$event)" :n="n"/>
    </div>
    <div class="row">
      <cell @click="onClickCell(3,$event)" :n="n"/>
      <cell @click="onClickCell(4,$event)" :n="n"/>
      <cell @click="onClickCell(5,$event)" :n="n"/>
    </div>
    <div class="row">
      <cell @click="onClickCell(6,$event)" :n="n"/>
      <cell @click="onClickCell(7,$event)" :n="n"/>
      <cell @click="onClickCell(8,$event)" :n="n"/>
    </div>
    </div>
    <h2>结果：{{result===null?'未见分晓，请继续落子':`胜方为${result},游戏结束`}}</h2>
  </div>
</template>

<script>
  import cell from './cell.vue'
  export default{
    components:{cell},
    data(){
      return {
        n:0,
        map:[
          [null,null,null],
          [null,null,null],
          [null,null,null]
        ],
        result:null
      }
    },
    methods:{
      onClickCell(i,text){
        console.log(`${i}号cell被点了，内容是：${text}`);
        this.map[Math.floor(i/3)][i%3]=text;
        this.n=this.n+1;
        this.tell()
      },
      tell(){
        const map=this.map;
        for(let i=0;i<2;i++){
          if(
            map[i][0]!==null &&
            map[i][0]===map[i][1] && 
            map[i][1]===map[i][2]
            ){
            this.result=map[i][0];
          }
        }
        for(let j=0;j<2;j++){
          if(
            map[0][j]!==null &&
            map[0][j]===map[1][j] && 
            map[1][j]===map[2][j]
            ){
            this.result=map[0][j];
          }
        }
        if(map[0][0]!==null && map[0][0]===map[1][1] && map[1][1]===map[2][2]){
          this.result=map[1][1]
        }
        if(map[0][2]!==null && map[0][2]===map[1][1] && map[1][1]===map[2][0]){
          this.result=map[1][1]
        }
      }
    }
  }
</script>
<style>
  .row{
    display:flex;
  }
  html,body,.wrapper{
    height:100%;
    padding:0;
    margin:0;
  }
  .wrapper{
    display:flex;
    flex-direction:column;
    justify-content:center;
    align-items:center;
    background-color:rgba(20,203,70,0.3)
  }
</style>
