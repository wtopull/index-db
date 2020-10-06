<template>
    <div id="app">
        <div>
            <small>添加前请先打开数据库(如数据库不存在则执行创建过程)</small><br /><br />
            <button @click="openDB">打开数据库</button>
            <button @click="deleteDB">删除数据库</button><br /><br />
            <button @click="closeDB">关闭数据库</button><br /><br />
            姓名：<input type="text" id="name" v-model="name"><br />
            年龄：<input type="number" id="age" min=1 v-model="age"><br />
            性别：
            男：<input type="radio" id="man" name="sex" value="male" v-model="sex">
            女：<input type="radio" id="woman" name="sex" value="female" v-model="sex"><br />

            <button @click="add">添加数据</button>
            <button @click="get">获取数据</button><br />
            <button @click="foreach">遍历数据</button><br />
            <button @click="update">更新数据</button><br />
            <button @click="remove">删除数据</button><input type="text" v-model.number="delIndex"><br />
            <button @click="searchFromIndex">根据索引查数据</button><br />
        </div>
    </div>
</template>

<script>
import indexedDB from "@/assets/indexedDB";
export default {
    data() {
        return {
            delIndex: null,
            name: "",
            age: 12,
            sex: "male",
        };
    },
    mounted() {},
    methods: {
        // 打开数据库
        openDB() {
            indexedDB.openDB("test", "person", 1);
        },
        // 删除数据库
        deleteDB() {
            indexedDB.deleteDB("test");
        },
        // 关闭数据库
        closeDB() {
            indexedDB.closeDB("test");
        },
        // 添加数据
        add() {
            indexedDB.add("person", {
                // name: this.name,
                // age: parseInt(this.age),
                // sex: this.sex,
                name: "开奖",
                qihao: 269,
                new_data: [
                    { num: 28, sx: "鸡", bs: "green" },
                    { num: 10, sx: "兔", bs: "blue" },
                    { num: 30, sx: "羊", bs: "red" },
                    { num: 16, sx: "鸡", bs: "green" },
                    { num: 25, sx: "鼠", bs: "blue" },
                    { num: 42, sx: "羊", bs: "blue" },
                    { num: 9, sx: "龙", bs: "blue" },
                ],
                nextdate: 1601991000,
                nextid: 270,
            });
        },
        // 获取数据
        get() {
            indexedDB.get("person");
        },
        // 遍历数据
        foreach() {
            indexedDB.foreach("person");
        },
        // 更新数据
        update() {
            indexedDB.update("person", {
                name: "大宝",
                age: 28,
                sex: "male",
                id: 4,
            });
        },
        // 删除数据
        remove() {
            indexedDB.remove("person", this.delIndex);
            this.delIndex = null;
        },
        // 根据索引查数据
        searchFromIndex() {
            indexedDB.searchFromIndex("person", "name");
        },
    },
};
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
}
</style>
