<template>
  <div>
    <ul>
      <!-- 로컬 스토리지 데이터 출력 -->
      <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shadow">
        <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}"
            v-on:click="toggleComplete(todoItem, index)"></i>
        <span v-bind:class="{textCompleted: todoItem.completed}">
          {{ todoItem.item }}
        </span>
        <span class="removeBtn" @click="removeTodo(todoItem, index)">
          <i class="far fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['propsdata'], // App.vue 에서 내려보낸 propsdata
  methods: {
    // 할 일 삭제 - 하위 컴포넌트 -> 상위 컴포넌트 (TodoList.vue -> App.vue)
    removeTodo(todoItem, index) {
      this.$emit('removeItem', todoItem, index);
    },
    // 할 일 완료 - 하위 컴포넌트 -> 상위 컴포넌트 (TodoList.vue -> App.vue)
    toggleComplete: function (todoItem, index) {
      this.$emit('toggleItem', todoItem, index);
    }
  }
}
</script>

<style scoped>
  ul {
    list-style-type: none;
    padding-left: 0;
    margin-top: 0;
    text-align: left;
  }

  li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
  }

  .checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
  }

  .checkBtnCompleted {
    color: #b3adad;
  }

  .textCompleted {
    text-decoration: line-through;
    color: #b3adad;
  }

  .removeBtn {
    margin-left: auto;
    color: #de4343;
  }
</style>
