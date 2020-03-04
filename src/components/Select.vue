<template>
  <div class="select">
    <div class="inner">
      <div class="inputWrapper" @click.stop="showOptions = !showOptions">
        <input type="text" readonly placeholder="请选择菜品" :value="selected">
        <span class="iconfont icon-zhankaishangxia"></span>
      </div>
      <ul class="options" v-show="showOptions" v-clickOut="test">
        <li
          v-for="(item, index) in options"
          :key="index"
          @click.stop="choose(item.value)"
        >{{item.value}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: [
        {
          value: "西红柿鸡蛋"
        },
        {
          value: "青椒抱鸡蛋"
        },
        {
          value: "回锅肉"
        },
        {
          value: "宫保鸡丁"
        },
        {
          value: "地三鲜"
        }
      ],
      showOptions: false,
      selected: ""
    };
  },
  methods: {
    choose(value) {
      this.showOptions = false;
      if (value !== this.selected) {
        this.selected = value;
      }
    },
    test() {
      this.showOptions = false;
    }
  },
  directives: {
    //这里是自定义指令
    clickOut: {
      // 这里是自定义的v-clickOut指令
      bind: function(el, binding) {
        // 如果点击的元素是被指令绑定的元素的子元素或是被绑定元素本身，那就什么都不做；如果不是，那就执行传递进来的test函数。
        function handler(e) {
          if (el.contains(e.target)) return false;
          if (binding.expression) {
            binding.value();
          }
        }
        el.handler = handler;
        document.addEventListener("click", el.handler);
      },
      unbind: function(el) {
        document.removeEventListener("click", el.handler);
      }
    }
  }
};
</script>


<style lang="scss" scoped>
$size: 14px;
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.ul,
ol,
li {
  list-style: none;
}
.inner {
  position: relative;
  margin: 0 auto;
  width: 300px;
  height: 30px;
  font-size: $size;
  border: 1px solid #a607f0;
  border-radius: 3px;
  .inputWrapper {
    width: 100%;
    height: 100%;
    background-color: #ddd;
    > input {
      width: 85%;
      height: 100%;
      padding-left: 10px;
      border: 1px solid #07d5f0;
      cursor: pointer;
    }
  }
  > .options {
    position: absolute;
    left: 0;
    right: 0;
    top: 150%;
    padding: 10px 0;
    background-color: rgb(228, 117, 26);
    box-shadow: 0 0 4px #ddd;
    border-radius: 3px;
    overflow: auto;
    > li {
      padding: 3px 10px;
      cursor: pointer;
      &:hover {
        background-color: rgb(4, 231, 220);
      }
    }
  }
}
</style>