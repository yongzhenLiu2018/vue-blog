<template>
  <div style="height: 100%">
    <head-nav></head-nav>
    <Aside></Aside>
    <div class="list-container main">
      <transition name="slide-fade">
        <div class="dialog-container" v-show="isDiaShow" @click="hideDialog($event)">
          <section class="dialog">
            <h5>输入书籍</h5>
            <star :score="score" id="score" @choose-star="chooseScore"></star>
            <input type="text" id="name" placeholder="输入书籍名称...">
            <input type="text" id="author" placeholder="输入作者...">
            <section class="btn-container">
              <button id="confirm" class="not-del" @click="confirmChange">确认</button>
              <button id="cancel" class="delete">取消</button>
            </section>
          </section>
        </div>
      </transition>
      <h2>
        阅读评论 /
        <span>ARTICLE LIST</span>
      </h2>
      <hr>
      <main>
        <section class="btn-container">
          <button id="add" class="not-del" @click="addBook()">添加书籍</button>
        </section>
      </main>

    </div>
  </div>
</template>

<script>
  import ArticleList from '@/components/common/ArticleList'
  import Editor from  '@/components/common/Editor'
  import Aside from  '@/components/common/Aside'
  import HeadNav from '@/components/common/HeadNav'
  import request from '@/utils/request'
  import moment from 'moment'
  moment.locale('zh-CN')
    export default {
      data() {
        return {
          books: [],
          isDiaShow: false,
          isEditing: false,
          editingId: '',
          editingIndex: '',
          score: 0
        }
      },
      name: "ReadingList",
      components:{
        ArticleList,
        Editor,
        Aside,
        HeadNav
      },
      methods:{
        addBook(){
          console.log(1)
        },
        hideDialog(){},
        chooseScore(){},
        confirmChange(){}
      }
    }
</script>


<style lang="scss" type="scss" lang="scss" scoped>
  @import "../assets/style/variable";
  main {
    height: calc(100% - 48px);
    padding: 0.5em 0;
    overflow: auto;
  }

  .rd-list {
    width: 100%;
    border-collapse: collapse;
    th {
      height: 3em;
      font-size: 1.6rem;
      border-bottom: 1px solid $word;
    }
    td {
      text-align: center;
      height: 4em;
      border-bottom: 1px dotted $word;
    }
    .col-1,
    .col-2,
    .col-4 {
      width: 20%;
    }

    .col-2,
    .col-3 {
      border-left: 1px dotted $word;
      border-right: 1px dotted $word;
    }
  }

  .dialog-container {
    @include flex;
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    min-width: 1024px;
    min-height: 900px;
    overflow: auto;
    background: rgba(0, 0, 0, 0.3);
    .dialog {
      @include flex($flow: column wrap, $justify: flex-start);
      width: 400px;
      height: 300px;
      background: $white;
      box-shadow: 0 3px 10px rgba(0, 0, 0, 0.6);
      border-top: 20px solid $base;
      border-radius: 5px;
      h5 {
        margin: 20px;
      }
      .star {
        margin-top: 0;
        /deep/ .star-item {
          width: 1.5em;
          height: 1.5em;
        }
      }
      input {
        margin-bottom: 15px;
        width: 200px;
        height: 2.5em;
        border-radius: 2px;
        border: 1px solid $special;
        outline-color: $base;
      }
      .btn-container {
        width: 200px;
        @include flex($justify: space-between);
      }
    }
  }

  .slide-fade-enter-active {
    transition: all 0.3s ease;
  }
  .slide-fade-leave-active {
    transition: all 0.6s cubic-bezier(1, 0.5, 0.8, 1);
  }
  .slide-fade-enter,
  .slide-fade-leave-to {
    transform: translateY(-900px);
    opacity: 0;
  }
</style>
