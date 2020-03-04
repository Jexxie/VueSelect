<template>
  <div class="select">
    <!-- 指令放到了这里 -->
    <div class="inner" v-clickOut="test">
      <div class="inputWrapper" @click="showOptions = !showOptions">
        <!-- 去掉修饰符.stop -->
        <!-- 当有多个Select的时候，只有点击了空白的其它地方的时候，展开的选项才都会消失，当其中一个选项展开再去选择另一个的时候，之前展开的选项不会被收起。产生这个问题的原因是点击input部分的时候被阻止冒泡了。只要把它去掉同时把指定指令绑定的元素扩大到整个select而不是仅是之前的options部分就行了，因为在指令里有了拦截。 -->
        <input type="text" readonly placeholder="请选择菜品" :value="selected">
        <span class="iconfont icon-zhankaishangxia"></span>
      </div>
      <ul class="options" v-show="showOptions">
        <li v-for="(item, index) in options" :key="index" @click="choose(item.value)">{{item.value}}</li>
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
      selected: "",
      showOptions: false
    };
  },
  methods: {
    choose(name) {
      this.showOptions = false;
      if (name !== this.selected) {
        this.selected = name;
        this.$emit("selected", name);
      }
    },
    outsideDirec() {
      this.showOptions = false;
    },
    test() {
      this.showOptions = false;
    },
    example2() {
      return "xxx";
    }
  },
  directives: {
    clickOut: {
      bind: function(el, binding) {
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
  width: 200px;
  height: 30px;
  font-size: $size;
  border: 1px solid #dddee1;
  border-radius: 3px;
  .inputWrapper {
    width: 100%;
    height: 100%;
    > input {
      width: 85%;
      height: 100%;
      padding-left: 10px;
      border: none;
      cursor: pointer;
    }
  }
  > .options {
    position: absolute;
    left: 0;
    right: 0;
    top: 120%;
    padding: 10px 0;
    background-color: #fff;
    box-shadow: 0 0 4px #ddd;
    border-radius: 3px;
    overflow: auto;
    > li {
      padding: 3px 10px;
      cursor: pointer;
      &:hover {
        background-color: #eee;
      }
    }
  }
}
</style>