<template>
  <div>
    <!-- 1. Jinja Template : 데이터를 보여주는 방식 -->
    <h1>Welcome to {{title2}} !</h1>

    <!-- 2. v-model : 사용자의 입력을 받아오는 법-->
    <!-- 2-1. 2way binding 써보기 -->
    <input type="text" v-model="input1"/>
    <!-- 2-2. 버튼 클릭하면 알럿 창 뜨게 해서 확인해보기 -->
    <button type="button" @click="getData">Get</button>
    <button type="button" @click="setData">Set</button>

    <select class="form-control" v-model="region">
      <!-- 2-3. 리스트 형태는  v-for로 룹을 돌릴 수 있음 -->
      <option :key="i" :value="d.v" v-for="(d,i) in options">{{d.t}}</option>
    </select>

    
    <!-- 3. v-for로 룹 돌려서 테이블 만들기 -->
    <!--
        3-1. v-if : 조건 안맞으면 아예 안보여줌(렌더링 안함)
            - 특정 조건이 일어났을때만 뭔가 보여줄때는 v-if를 추천
            - 초기 화면에 렌더링을 안해도 되니까, 오히려 리소스가 효율적이다.
    -->
    <table class="table table-bordered" v-if="tableShow">
        <tr :key="i" v-for="(d,i) in options">
        <td>{{d.v}}</td>
        <td>{{d.t}}</td>
        </tr>
    </table>
    <!-- 
      3-2. v-show: 렌더링은 되는데 화면에 안보여줌.
        - 렌더링 자체에 리소스가 많이 들어감.
        - vshow는 렌더링은 했지만 스타일로 보이고/안보이고 처리를 함.
        - 따라서 리소스를 효율적으로 사용할 수 있다.
        - 빈번하게 보였다/안보였다가 일어나면 vshow 추천
    -->
      <table class="table table-bordered" v-show="tableShow">
      <tr :key="i" v-for="(d,i) in options">
      <td>{{d.v}}</td>
      <td>{{d.t}}</td>
      </tr>
  </table>
  </div>
</template>
<script>
// 데이터를 핸들링 하는 부분
export default {
  // 메소드를 정의하고, 리턴 해보기
  data(){
    // 리턴하는 파라미터를 통해서, 진자 템플릿에 바인딩 됨
    return {
      title : "개발자의 품격",
      title2 : "Seoul",
      // vue js 는 two-way 바인딩을 지원
      // --> 정의된 데이터를 화면에 보여주기도 하고, 화면에 있는 값을 컨트롤 할 수도 있음.
      input1 : "abcd",
      options : [
        // 배열 다뤄보기
        {v : "S", t : "Seoul"},
        {v : "J", t : "Jeju"},
        {v : "B", t : "Busan"}
      ],
      region : "J",
      tableShow: false
    };
  },
  methods:{
    // 1. 특정 이벤트를 메서드로 처리 해 보기
    getData(){
      // 버튼을 누르면, 알럿이 뜨는 메서드
      alert(this.input1);
    },
    setData(){
      this.input1="12345";
    },
    changeRegion(){
      alert(this.region);
    },
    // 2. watch 사용해보기
    watch : {
      // watch에서 데이터명으로 function을 만들 수 있다.
      input1 (){
        // input1이라는 데이터에 조금이라도 변경이 생기면
        // 같은 이름의 watch 내의 펑션 내에서 캐치해서 알 수 있다.
        console.log(this.input1);
      }
    },

    // 3. 뷰 라이프사이클대로 찍어보기(브라우저에서 확인)
    // 이 메소드를 알아두면, 라이프사이클의 변경(컴포넌트 추가/생성/삭제)에 따라 이벤트를 처리할 수 있음.
    beforeCreate() {
      console.error("beforeCreate");
    },
    created(){
      console.error("created");
    },
    beforeMount(){
      // 만약에 DB에서 뭔가를 가져와서 한번에 화면에 보여줘야 한다면, 마운트 되기 전에 다 처리하고
      // 마운트 됐을 때 한번에 보여주면 좋음.
      console.error("beforeMount");
    },
    mounted() {
      console.error("mounted");
    },
    beforeUpdate(){
      console.log("beforeUpdate");
    },
    updated() {
      console.error("updated");
    },
    beforeDestroy() {
      console.error("beforeDestroy");
    },
    destroyed() {
      console.error("destroyed");
    },
  }
};
</script>