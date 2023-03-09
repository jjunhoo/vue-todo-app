<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      newTodoItem: '' // input box 입력값
    }
  },
  methods: {
    // 하위 컴포넌트 -> 상위 컴포넌트 (TodoInput.vue -> App.vue)
    addTodo: function() {
      if (this.newTodoItem !== '') { // 입력값이 있는 경우, 저장
        this.$emit('addTodoItem', this.newTodoItem) // 상위 컴포넌트로 데이터 전달 (App.vue)
        this.clearInput(); // input box 입력값 초기화
      }
    },
    clearInput: function () {
      this.newTodoItem = '';
    }
  }
}
</script>

<style scoped>
  input:focus {
    outline: none;
  }
  .inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  .inputBox input {
    border-style: none;
    font-size: 0.9rem;
  }
  .addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
  }
  .addBtn {
    color: white;
    vertical-align: middle;
  }
</style>
