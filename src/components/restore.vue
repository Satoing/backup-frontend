<template>
    <li v-for="file in files">{{file}}</li>
    <el-input v-model="input" placeholder="输入你要还原的路径" />
    <el-button @click="submitFileAndPath">提交</el-button>
</template>

<script>
export default {
  data() {
    return {
      input: '',
      files: ["1", "2", "3"]
    }
  },
  methods: {
    // 提交文件
    submitFileAndPath() {
        console.log(this.input);
        console.log(this.files);
    }
  },
};
</script>