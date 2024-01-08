<template>
    <div v-if="!submited">
        <el-input v-model="path" placeholder="输入你要备份的路径" />
        <el-button @click="submitPath">提交</el-button>
    </div>
    <div v-if="submited">
        <div>
            <el-checkbox v-model="file.value" v-bind:label="file.name" size="large" v-for="file in files"/>
        </div>
        <el-button @click="submitFiles">提交</el-button>
    </div>
    <p style="font-color: red;" v-if="iserror">提交失败，请重试</p>
    <p style="font-color: red;" v-if="pushok">提交成功！</p>
</template>

<script>
import axios from 'axios'
import qs from 'qs'

export default {
  data() {
    return {
        path: '',
        submited: false,
        // 文件列表格式
        files: [
            {name: "示例1", value: 1},
            {name: "示例2", value: 0},
            {name: "示例3", value: 1},
        ],
        iserror: false,
        pushok: false,
    }
  },
  methods: {
    // 提交路径
    submitPath() {
        axios.get("http://127.0.0.1:5000/getfiles?path="+this.path).then(resp=>{
            this.files = [];
            if(resp.data == "-1") this.iserror = true;
            const filelist = resp.data;
            for(let file of filelist) {
                this.files.push({name: file, value: true});
            }
            this.submited = true;
        })
    },
    // 提交文件
    submitFiles() {
        let filelist = [];
        for(let file of this.files) {
            if(file.value) {
                filelist.push(file.name);
            }
        }
        axios.post(`http://127.0.0.1:5000/backupfiles`, qs.stringify(filelist)).then(resp=>{
            if(resp.data == '0') {
                this.pushok = true
            }
            else {
                this.iserror = true;
            }
        })
    }
  },
};
</script>

<style>
.el-checkbox--large{
    display: block;
}
</style>