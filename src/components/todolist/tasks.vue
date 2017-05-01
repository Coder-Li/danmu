<template>
  <div class="tasks">
    <div class="header">待办事项</div>
    <div class="text-add">
      <input type="text" placeholder="输入待办事项" v-model="inputText"
             @keyup.enter="addNewTodo">
    </div>
    <div class="list">
      <div class="todo-list">
        <div class="item" v-for="item in lists" :key="item" v-if="!item.isFinished">
          <input @click="toggleState(item)" type="checkbox"><span class="text">{{item.text}}</span><span
          class="del" @click="remove(item)">删除</span>
        </div>
      </div>
      <div class="done-list">
        <div class="item" v-for="item in doneList" :key="item" v-if="item.isFinished">
          <input checked="checked" @click="toggleState(item)" type="checkbox">
          <span class="text">{{item.text}}</span><span
          class="del" @click="remove(item)">删除</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default{
    data() {
      return {
        inputText: '',
        lists: []
      }
    },
    methods: {
      addNewTodo: function () {
        if (this.inputText === '') {
          return;
        }
        this.lists.push({text: this.inputText, isFinished: false});
        this.inputText = '';
      },
      toggleState: function (item) {
        item.isFinished = !item.isFinished;
      },
      remove: function (item) {
        console.log('del');
        this.lists = this.lists.filter((i) => {
          return !(i === item);
        });
        console.log(this.lists);
      }
    },
    computed: {
      doneList: function () {
        return this.lists.filter((item) => {
          return item.isFinished;
        })
      }
    }
  }
</script>

<style lang="stylus">
  .tasks
    position: absolute;
    display: block;
    width: 300px;
    height: 500px;
    top: 50%;
    left: 50%;
    margin-top: -250px;
    margin-left: -150px;
    border: 1px solid #000000;
    .header
      width: 100%;
      text-align: center;
      line-height: 30px
      height: 30px;
      font-weight: 900
      margin-bottom: 10px;
    .text-add
      width: 100%
      text-align center
      margin-bottom: 10px;
      input
        margin-left: 10px;
        height: 28px;
        font-size: 22px;
        padding: 3px 0;
    .list
      border-top: 1px solid rgba(7, 17, 27, .2);
      height: 412px;
      width: 100%;
      .todo-list, .done-list
        margin-top: 2px;
        height: 204px;
        overflow: auto;
        .item
          display: inline-block
          height: 30px;
          line-height: 30px;
          width: 90%;
          font-size: 22px;
          white-space: nowrap
          overflow: hidden;
          box-shadow: 2px 2px 2px rgba(0, 0, 0, .3);
          margin: 0 5%;
          box-sizing: border-box;
          input[type=checkbox]
            margin-top: 4px;
            margin-right: 6px;
            line-height: 30px;
            width: 20px;
            height: 20px;
            vertical-align: top
          span
            display: inline-block;
            vertical-align top;
          .del
            float: right;
            cursor: pointer;
            color: blue;
            margin-right: 10px;
      .todo-list
        border-bottom: 1px solid rgba(7, 17, 27, .2)
</style>
