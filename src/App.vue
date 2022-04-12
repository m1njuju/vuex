<template>
  <div id="app">
    <!-- $store.state.count를 통해서 바로 값을 들고 올 수 있다 -->
    <h1>카운터에서 가져온 값입니다 {{count}}</h1>
    <button @click="$store.commit('addcount')">추가</button>
    <button @click="addcount">추가</button>
    <button @click="addcountaction">추가(Action)</button>
    <button @click="timer">1초 뒤 추가(Action)</button>
    <button @click="ntimer({count:50, time:10000})">10초 뒤 추가(Action)</button>

    <!-- 버튼을 누르면 1초마다 count값이 1씩 증가하는 Action을 만들어서 추가 -->
    <!-- setInterval -->
    <button @click="timersecond"> 1초 마다 1 증가</button>

    <!-- 버튼을 누르면 1 감소하는 버튼을 추가 -->
    <button @click="$store.commit('subcount')">감소</button>

    <ul>
      <li v-for="list in $store.state.list" :key="list.id">{{list.memo}}</li>
    </ul>

    <!-- index.js에 name : ['홍길동','성춘향','그린']을 추가하고 -->
    <!-- 아래에 computed를 이용하여 간략하게 만들어 출력 -->
    <ul>
      <li v-for="(n,i) in names" :key="i">{{n}}</li>
    </ul>

    <p>{{ doneTodosCount }}</p>
    <p>{{ doneTodosCountGetter }}</p>

    <HelloWorld />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  computed: {
    //머스테치 안의 내용이 길어지면 computed를 통해서 출력해 줄 수 있다
    count: function() {
      return this.$store.state.count;
    },
    names: function() {
      return this.$store.state.name;
    },
    doneTodosCount: function() {
      return this.$store.state.todos.filter( todo => todo.done ).length;
    },
    doneTodosCountGetter: function() {
      // store getters를 통해 계산된 내용을 컴포넌트마다 가져와서 사용
      return this.$store.getters.doneTodosCountGetter;
    }
  },
  methods: {
    // Mutation의 메서드는 commit을 통해 들고온다
    addcount: function() {
      this.$store.commit('addcount');
    },
    // Action의 메서드는 dispatch를 통해 들고온다
    addcountaction: function() {
      this.$store.dispatch('addcount');
    },
    timer: function() {
      this.$store.dispatch('timer');
    },
    ntimer: function(time) {
      this.$store.dispatch('ntimer', time);
    },
    timersecond: function() {
      this.$store.dispatch('timersecond');
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
