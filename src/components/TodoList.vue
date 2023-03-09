<template>
  <section>
    <ul>
      <!-- 로컬 스토리지 데이터 출력 -->
      <li v-for="(todoItem, index) in todoItems" class="shadow">
        <i class="checkBtn fas fa-check aria-hidden="true"></i>
        {{ todoItem }}
        <span class="removeBtn" type="button" @click="removeTodo(todoItem, index)">
          <i class="far fa-trash-alt" aria-hidden="true"></i>
        </span>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  data() {
    return {
      todoItems: []
    }
  },
  created() {
    // 로컬 스토리지에 저장된 데이터가 있는 경우, todoItems 배열에 저장
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  methods: {
    // 할 일 삭제
    removeTodo(todoItem, index) {
      // 로컬 스토리지 삭제
      localStorage.removeItem(todoItem);
      // 로컬 스토리지 내부 뷰 변수 삭제
      this.todoItems.splice(index, 1); // 배열의 해당 인덱스에서 1만큼 삭제
    }
  }
}
</script>

<style scoped>
  ul {
    list-style-type: none;
    padding-left: 0px;
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

  .removeBtn {
    margin-left: auto;
    color: #de4343;
  }
</style>
