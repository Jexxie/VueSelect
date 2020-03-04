<template>
  <div class="select">
    <div style="marginTop: 200px; display: flex;">
      <Select/>
      <Select/>
    </div>
  </div>
</template>

<script>
import Select from "./Select";
export default {
  name: "HelloWorld",
  components: {
    Select
  }
};
</script>

<style scoped>
ul,
li {
  list-style: none;
}
.select {
  position: relative;
  padding-left: 100px;
}
.wrapper {
  position: relative;
  width: 200px;
  height: 30px;
  border: 1px solid #dddee1;
  border-radius: 3px;
  cursor: pointer;
}
.icon {
  position: absolute;
  top: 50%;
  right: 8px;
  transform: translateY(-50%);
}
.wrapper > .options {
  width: 100%;
}
.wrapper > input {
  padding-left: 10px;
  width: 85%;
  height: 100%;
  font-size: 14px;
  border: none;
  cursor: pointer;
}
.wrapper > input:focus {
  outline: none;
}
.options {
  position: absolute;
  left: 0;
  top: 125%;
  width: 100%;
  padding: 5px 0;
  font-size: 14px;
  border-radius: 3px;
  box-shadow: 0 0 4px #ddd;
  overflow: auto;
}
.options > li {
  padding: 5px 10px;
  cursor: pointer;
  white-space: nowrap;
}
.options > li:hover {
  background-color: #f3f3f3;
}
</style>