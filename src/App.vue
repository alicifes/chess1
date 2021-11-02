<template>
  <div class="wrapper">
    <div>当前为第{{n}}手</div>
    <div class="chess">
      <div class="row">
        <Cell @click="onCLickCell(0, $event)" :n="n"/>
        <Cell @click="onCLickCell(1, $event)" :n="n"/>
        <Cell @click="onCLickCell(2, $event)" :n="n"/>
      </div>
      <div class="row">
        <Cell @click="onCLickCell(3, $event)" :n="n"/>
        <Cell @click="onCLickCell(4, $event)" :n="n"/>
        <Cell @click="onCLickCell(5, $event)" :n="n"/>
      </div>
      <div class="row">
        <Cell @click="onCLickCell(6, $event)" :n="n"/>
        <Cell @click="onCLickCell(7, $event)" :n="n"/>
        <Cell @click="onCLickCell(8, $event)" :n="n"/>
      </div>
      
      <div>目前的结果为：{{map}}</div>
      <div>结果：{{result==null?'胜负未分':`胜方为${result}`}}</div>
    </div>
  </div>
</template>

<script>
import Cell from './components/Cell.vue'
export default {
  components:{Cell},
  data(){
    return{
      n:0,
      map:[
        [null,null,null],
        [null,null,null],
        [null,null,null]
      ],
      result:null
    }
  },
  methods: {
    onCLickCell(i,text){
      this.n+=1
      this.map[Math.floor(i/3)][i%3] = text   //将东西填入到对应的项内部
      // console.log(this.map);
      // console.log(`${i}被打印了,值是${text}`)
      this.tell()
    },
    tell(){
      for(let i = 0 ;i<2;i++){
        if(this.map[i][0]!=null&&this.map[i][0]==this.map[i][1]&&this.map[i][1]==this.map[i][2]){
          this.result = this.map[i][0]
        }
      }
      for(let j = 0 ;j<2;j++){
        if(this.map[0][j]!=null&&this.map[0][j]==this.map[1][j]&&this.map[1][j]==this.map[2][j]){
          this.result = this.map[0][j]
        }
      }
      if(this.map[0][0]!=null&&this.map[0][0]==this.map[1][1]&&this.map[1][1]==this.map[2][2]){   //需要判断第一项是否为空
        this.result = this.map[0][0]
      }
      if(this.map[0][2]!=null&&this.map[0][2]==this.map[1][1]&&this.map[1][1]==this.map[2][0]){   //需要判断第一项是否为空
        this.result = this.map[0][2]
      }
    }
  }
}
</script>

<style>
.wrapper{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.row{
  display: flex;
}
</style>
